---
title: Mejorar la seguridad de AEM Forms en el entorno JEE
description: Conozca diferentes configuraciones de seguridad para mejorar la seguridad de AEM Forms en un entorno JEE que se ejecuta en una intranet corporativa.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '7605'
ht-degree: 90%

---

# Mejorar la seguridad de AEM Forms en el entorno JEE {#hardening-your-aem-forms-on-jee-environment}

Conozca diferentes configuraciones de seguridad para mejorar la seguridad de AEM Forms en un entorno JEE que se ejecuta en una intranet corporativa.

El artículo contiene recomendaciones y prácticas recomendadas para proteger los servidores que ejecutan AEM Forms en JEE. El objetivo de este documento no es proporcionar una guía completa sobre cómo proteger el host del sistema operativo y los servidores de aplicaciones. En vez de eso, este artículo describe las diferentes configuraciones de seguridad que debe implementar para mejorar la seguridad de AEM Forms en entornos JEE que se ejecutan en una intranet corporativa. Sin embargo, para asegurarse de que AEM Forms sigue siendo seguro en los servidores de aplicaciones JEE, también debe implementar procedimientos de monitorización, detección y respuesta de seguridad.

El artículo describe las técnicas de protección que deben aplicarse durante las siguientes etapas del ciclo de vida de instalación y configuración:

* **Preinstalación:** utilice estas técnicas antes de instalar AEM Forms en JEE.
* **Instalación:** utilice estas técnicas durante el proceso de instalación de AEM Forms en JEE.
* **Después de la instalación:** utilice estas técnicas después de la instalación y posteriormente de forma periódica.

AEM Forms en JEE ofrece un alto grado de personalización y es compatible con un gran número de entornos diferentes. Es posible que algunas de las recomendaciones no se ajusten a las necesidades de la organización.

## Preinstalación {#preinstallation}

Antes de instalar AEM Forms en JEE, puede aplicar las soluciones de seguridad en la capa de red y el sistema operativo. Esta sección describen algunos problemas e incluye recomendaciones para reducir las vulnerabilidades de seguridad en estas áreas.

**Instalación y configuración en UNIX y Linux**

No debe instalar ni configurar AEM Forms en JEE con un shell raíz. De forma predeterminada, los archivos se instalan en el directorio /opt, y el usuario que realiza la instalación necesita todos los permisos de archivo en /opt. Como alternativa, se puede realizar una instalación en el directorio /user de un usuario individual en el que ya se tengan todos los permisos de archivo.

**Instalación y configuración en Windows**

Debe realizar la instalación en Windows como administrador si está instalando AEM Forms en un entorno JEE de JBoss mediante el método llave en mano, o si está instalando PDF Generator. Además, al instalar PDF Generator en Windows con compatibilidad con aplicaciones nativas, debe ejecutar la instalación con el mismo usuario de Windows que instaló Microsoft Office. Para obtener más información sobre los privilegios de instalación, consulte el documento* Instalación e implementación de AEM Forms en JEE* para su servidor de aplicaciones.

### Seguridad de capa de red {#network-layer-security}

Las vulnerabilidades de seguridad de red están entre las principales amenazas a las que está expuesto un servidor de aplicaciones orientado a Internet o a la intranet. Esta sección describe el proceso de protección de los hosts de la red frente a este tipo de vulnerabilidades. Aborda la segmentación de red, la protección de pila del Protocolo de control de transmisión/Protocolo Internet (TCP/IP) y el uso de cortafuegos para la protección del host.

En la tabla siguiente se describen algunos procesos comunes que reducen las vulnerabilidades de seguridad de red.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zonas desmilitarizadas (DMZ)</p> </td> 
   <td><p>Implementar servidores de formularios en una zona desmilitarizada (DMZ). La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones utilizado para ejecutar AEM Forms en JEE detrás del cortafuegos interno. Separe la red externa de la DMZ que contiene los servidores web, que a su vez deben separarse de la red interna. Utilice cortafuegos para implementar las capas de separación. Categorice y controle el tráfico que pasa por cada capa de red para asegurarse de que solo se permite el mínimo absoluto de datos requerido.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Direcciones IP privadas</p> </td> 
   <td><p>Utilice la traducción de direcciones de red (NAT) con direcciones IP privadas (RFC 1918) en el servidor de aplicaciones de AEM Forms. Asigne direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Cortafuegos</p> </td> 
   <td><p>Utilice los siguientes criterios para seleccionar una solución de cortafuegos:</p> 
    <ul> 
     <li><p>Implemente servidores de seguridad que admitan servidores proxy o <em>inspección de estado</em> en lugar de soluciones simples de filtrado de paquetes.</p> </li> 
     <li><p>Utilice un cortafuegos compatible con los paradigmas de seguridad <em>Denegar todos los servicios excepto los expresamente permitidos</em>.</p> </li> 
     <li><p>Implemente una solución de cortafuegos de doble alojamiento o multialojamiento. Esta arquitectura proporciona el máximo nivel de seguridad y ayuda a evitar que usuarios no autorizados eludan la seguridad del firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Puertos de base de datos</p> </td> 
   <td><p>No utilice puertos de escucha predeterminados para bases de datos (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Para obtener información sobre cómo cambiar los puertos de base de datos, consulte la documentación de la base de datos.</p> <p>El uso de un puerto de base de datos diferente afecta a la configuración general de AEM Forms en JEE. Si cambia los puertos predeterminados, debe realizar las modificaciones correspondientes en otras áreas de configuración, como las fuentes de datos de AEM Forms en JEE.</p> <p>Para obtener información sobre la configuración de fuentes de datos de AEM Forms en JEE, consulte Instalación y actualización de AEM Forms en JEE o Actualización a AEM Forms en JEE para su servidor de aplicaciones en la <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guía del usuario de AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Seguridad del sistema operativo {#operating-system-security}

La siguiente tabla describe algunos de los enfoques que puede adoptar para minimizar las vulnerabilidades de seguridad presentes en el sistema operativo.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p></th> 
   <th><p>Descripción</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Parches de seguridad</p></td> 
   <td><p>El riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones aumenta si los parches y las actualizaciones de seguridad del proveedor no se aplican de forma oportuna. Pruebe los parches de seguridad antes de aplicarlos a los servidores de producción.</p><p>Asimismo, cree políticas y procedimientos para buscar e instalar los parches de forma regular.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software de protección antivirus</p></td> 
   <td><p>Los analizadores de virus pueden identificar los archivos infectados mediante la búsqueda de una firma o la observación de comportamientos inusuales. Los analizadores guardan sus firmas de virus en un archivo que suele almacenarse en el disco duro local. Dado que se descubren virus nuevos con frecuencia, debe actualizar este archivo para que el analizador de virus identifique todos los virus actuales.</p></td> 
  </tr> 
  <tr> 
   <td><p>Protocolo de tiempo de redes (NTP)</p></td> 
   <td><p>Mantenga la precisión horaria en los servidores de Forms para realizar el análisis forense. Utilice el NTP para sincronizar la hora en todos los sistemas conectados directamente a Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Para obtener información de seguridad adicional sobre su sistema operativo, consulte [&quot;Información de seguridad del sistema operativo&quot;](https://helpx.adobe.com/es/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Instalación {#installation}

Esta sección describe las técnicas que puede utilizar durante el proceso de instalación de AEM Forms para reducir las vulnerabilidades de seguridad. En algunos casos, estas técnicas utilizan opciones incluidas en el proceso de instalación. La tabla siguiente describe estas técnicas.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Privilegios</p> </td> 
   <td><p>Utilice el menor número de privilegios necesarios para instalar el software. Inicie sesión en el equipo con una cuenta que no forme parte del grupo Administradores. En Windows, puede utilizar el comando Ejecutar como para ejecutar el programa de instalación de AEM Forms en JEE como usuario administrativo. En sistemas UNIX y Linux, utilice un comando como <code>sudo</code> para instalar el software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fuente del software</p> </td> 
   <td><p>No descargue ni ejecute AEM Forms en JEE desde fuentes que no sean de confianza.</p> <p>Los programas maliciosos pueden contener código para infringir la seguridad de varias formas, incluido el robo, la modificación y la eliminación de datos y la denegación de servicio. Instale AEM Forms en JEE desde el DVD de Adobe o únicamente desde una fuente de confianza.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Particiones de disco</p> </td> 
   <td><p>Instale AEM Forms en JEE en una partición de disco dedicada. La segmentación de discos es un proceso que mantiene datos específicos del servidor en discos físicos separados para proporcionar una mayor seguridad. Organizar los datos de esta forma reduce el riesgo de ataques transversales de directorios. Planee la creación una partición independiente de la partición del sistema en la que pueda instalar el directorio de contenido de AEM Forms en JEE. (En Windows, la partición del sistema contiene el directorio system32 o la partición de arranque).</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componentes</p> </td> 
   <td><p>Evalúe los servicios existentes y deshabilite o desinstale los que no sean necesarios. No instale componentes y servicios innecesarios.</p> <p>La instalación predeterminada de un servidor de aplicaciones puede incluir servicios que no son necesarios para su uso. Debe deshabilitar todos los servicios innecesarios antes de la implementación para minimizar los puntos de entrada de un ataque. Por ejemplo, en JBoss, puede comentar servicios innecesarios en el archivo descriptor META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Archivo de política entre dominios</p> </td> 
   <td><p>La presencia de un archivo <code>crossdomain.xml</code> en el servidor puede debilitar inmediatamente dicho servidor. Se recomienda que la lista de dominios sea lo más restrictiva posible. No coloque el archivo <code>crossdomain.xml</code> que se utilizó durante el desarrollo en producción cuando use las guías <em>(obsoleto)</em>. En el caso de las guías que utilizan servicios web, si el servicio se encuentra en el mismo servidor que proporcionó la guía, no es necesario el archivo <code>crossdomain.xml</code>. Sin embargo, si el servicio está en otro servidor, o si hay clústeres implicados, su presencia de un archivo <code>crossdomain.xml</code> sí es necesaria. Consulte <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a> para obtener más información sobre el archivo cross-domain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configuración de seguridad del sistema operativo</p> </td> 
   <td><p>Si necesita utilizar codificación XML de 192 o 256 bits en plataformas Solaris, asegúrese de instalar <code>pkcs11_softtoken_extra.so</code> en lugar de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Pasos posteriores a la instalación {#post-installation-steps}

Después de instalar correctamente AEM Forms en JEE, es importante mantener periódicamente el entorno desde el punto de vista de la seguridad.

En la siguiente sección se describen en detalle las diferentes tareas recomendadas para proteger el servidor de Forms implementado.

### Seguridad de AEM Forms {#aem-forms-security}

Las siguientes configuraciones recomendadas se aplican al servidor de AEM Forms en JEE fuera de la aplicación web administrativa. Para reducir los riesgos de seguridad a los que está expuesto el servidor, aplique esta configuración inmediatamente después de instalar AEM Forms en JEE.

**Parches de seguridad**

El riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones aumenta si los parches y las actualizaciones de seguridad del proveedor no se aplican de forma oportuna. Pruebe los parches de seguridad antes de aplicarlos a los servidores de producción para garantizar la compatibilidad y disponibilidad de las aplicaciones. Asimismo, cree políticas y procedimientos para buscar e instalar los parches de forma regular. Las actualizaciones de AEM Forms en JEE se encuentran en el sitio de descarga de productos empresariales.

**Cuentas de servicio (llave en mano de JBoss solo en Windows)**

De forma predeterminada, AEM Forms en JEE instala un servicio mediante la cuenta LocalSystem. La cuenta de usuario integrada de LocalSystem tiene un alto nivel de accesibilidad y forma parte del grupo Administradores. Si se ejecuta una identidad de proceso de trabajo como la cuenta de usuario LocalSystem, ese proceso de trabajo tiene acceso completo a todo el sistema.

Para ejecutar el servidor de aplicaciones en el que se implementa AEM Forms en JEE utilizando una cuenta específica no administrativa, siga estas instrucciones:

1. En Microsoft Management Console (MMC), cree un usuario local para que el servicio Forms Server inicie sesión como:

   * Seleccione **El usuario no puede cambiar la contraseña**.
   * En la pestaña **Miembro de**, asegúrese de que el grupo **Usuarios** aparece en la lista.

   >[!NOTE]
   >
   >No puede cambiar esta configuración para PDF Generator.

1. Seleccione **Inicio** > **Configuración** > **Herramientas administrativas** > **Servicios**.
1. Haga doble clic en JBoss para AEM Forms en JEE y detenga el servicio.
1. En la pestaña **Inicio de sesión**, seleccione **Esta cuenta**, busque la cuenta de usuario que ha creado e introduzca su contraseña.
1. En MMC, abra **Configuración de seguridad local** y seleccione **Directivas locales** > **Asignación de derechos de usuario**.
1. Asigne los siguientes derechos a la cuenta de usuario en la que se ejecuta el servidor de Forms:

   * Denegar el inicio de sesión a través de Terminal Services
   * Denegar el inicio de sesión de forma local
   * Iniciar sesión como servicio (ya debería estar configurado)

1. Asigne a la nueva cuenta de usuario permisos de modificación en los siguientes directorios:
   * **Directorio Global Document Storage (GDS)**: la ubicación del directorio GDS se configura manualmente durante el proceso de instalación de AEM Forms. Si la configuración de la ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones en `[JBoss root]/server/[type]/svcnative/DocumentStorage`.
   * **Directorio CRX-Repository**: la ubicación predeterminada es `[AEM-Forms-installation-location]\crx-repository`.
   * **Directorios temporales de AEM Forms**:
      * (Windows) Ruta TMP o TEMP tal como se establece en las variables de entorno
      * (AIX, Linux o Solaris) Directorio raíz del usuario que ha iniciado sesión
En sistemas basados en UNIX, un usuario no raíz puede utilizar el siguiente directorio como directorio temporal:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Asigne permisos de escritura a la nueva cuenta de usuario en los siguientes directorios:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >La ubicación de instalación predeterminada del servidor de aplicaciones JBoss:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/

1. Inicie el servidor de aplicaciones.

**Desactivación del servlet de arranque del Administrador de configuración**

El Administrador de configuración utilizó un servlet implementado en su servidor de aplicaciones para llevar a cabo el arranque de AEM Forms en la base de datos JEE. Dado que el Administrador de configuración accede a este servlet antes de que se complete la configuración, el acceso a él no se ha protegido para los usuarios autorizados y debe deshabilitarse después de haber utilizado correctamente el Administrador de configuración para configurar AEM Forms en JEE.

1. Descomprima el archivo adobe-livecycle-[appserver].ear.
1. Abra el archivo META-INF/application.xml.
1. Busque la sección adobe-bootstrapper.war:

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. Detenga el servidor de AEM Forms.
1. Comente los módulos adobe-bootstrapper.war y adobe-lcm-bootstrapper-redirectory.war como se indica a continuación:

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. Guarde y cierre el archivo META-INF/application.xml.
1. Comprima el archivo EAR y vuelva a implementarlo en el servidor de aplicaciones.
1. Inicie el servidor de AEM Forms.
1. Escriba la siguiente URL en un explorador para probar el cambio y asegurarse de que ya no funciona.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Bloqueo del acceso remoto al Almacén de confianza**

El Administrador de configuración permite cargar una credencial de extensiones de Acrobat Reader DC en el almacén de confianza de AEM Forms en JEE. Esto significa que el acceso al servicio de credenciales del Almacén de confianza a través de protocolos remotos (SOAP y EJB) se ha habilitado de forma predeterminada. Este acceso ya no es necesario después de cargar las credenciales de derechos mediante el Administrador de configuración, o si decide utilizar la consola de administración más adelante para administrar las credenciales.

Puede deshabilitar el acceso remoto a todos los servicios del Almacén de confianza siguiendo los pasos de la sección [Desactivación del acceso remoto no esencial a los servicios](https://helpx.adobe.com/es/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Desactive todo acceso anónimo no esencial**

Algunos servicios de Forms Server tienen operaciones que un llamador anónimo puede invocar. Si no se requiere acceso anónimo a estos servicios, deshabilite el acceso siguiendo los pasos indicados en [Desactivación del acceso anónimo no esencial a los servicios](https://helpx.adobe.com/es/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Cambiar la contraseña de administrador predeterminada {#change-the-default-administrator-password}

Cuando se instala AEM Forms en JEE, se configura una sola cuenta de usuario predeterminada para el usuario Super Administrator/ login-id Administrator con la contraseña predeterminada *password*. Debe cambiar esta contraseña inmediatamente usando el Administrador de configuración.

1. Escriba la siguiente URL en un explorador web:

   ```java
   https://[host name]:[port]/adminui
   ```

   El número de puerto predeterminado es uno de los siguientes:

   **JBoss:** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080

1. En el campo **Nombre de usuario**, escriba `administrator` y, en el campo **Contraseña**, escriba `password`.
1. Haga clic en **Configuración** > **User Management** > **Usuarios y grupos**.
1. Escriba `administrator` en el campo **Buscar** y haga clic en **Buscar**.
1. Haga clic en **Super Administrator** en la lista de usuarios.
1. Haga clic en **Cambiar contraseña** en la página Editar usuario.
1. Especifique la nueva contraseña y haga clic en **Guardar**.

Además, se recomienda cambiar la contraseña predeterminada del Administrador CRX realizando los siguientes pasos:

1. Inicie sesión en `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` usando el nombre de usuario/contraseña predeterminado.
1. Escriba Administrator en el campo de búsqueda y haga clic en **Ir**.
1. Seleccione **Administrator** en el resultado de búsqueda y haga clic en el botón **Editar** de la parte inferior derecha de la interfaz de usuario.
1. Especifique la nueva contraseña en el campo **Nueva contraseña** y la contraseña antigua en el campo **Su Contraseña**.
1. Haga clic en el icono Guardar en la parte inferior derecha de la interfaz de usuario.

#### Deshabilitar la generación de WSDL {#disable-wsdl-generation}

La generación del lenguaje de definición de servicios web (WSDL) solo debe habilitarse en entornos de desarrollo, donde los desarrolladores la utilizan para generar aplicaciones cliente. Puede optar por deshabilitar la generación de WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

1. Escriba la siguiente URL en un explorador web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Seleccione **Configuración > Configuración del sistema principal > Configuraciones**.
1. Anule la selección de **Habilitar WSDL** y, a continuación, seleccione **Aceptar**.

### Seguridad del servidor de aplicaciones {#application-server-security}

En la tabla siguiente se describen algunas técnicas para proteger el servidor de aplicaciones después de instalar la aplicación AEM Forms en JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Consola administrativa del servidor de aplicaciones</p> </td> 
   <td><p>Después de instalar, configurar e implementar AEM Forms en JEE en el servidor de aplicaciones, debe deshabilitar el acceso a las consolas administrativas del servidor de aplicaciones. Consulte la documentación del servidor de aplicaciones para obtener más información.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configuración de las cookies del servidor de aplicaciones</p> </td> 
   <td><p>El servidor de aplicaciones controla las cookies de las aplicaciones. Al implementar la aplicación, el administrador del servidor de aplicaciones puede especificar las preferencias de cookies en un servidor o en una aplicación específica. La configuración del servidor tiene preferencia de forma predeterminada.</p> <p>Todas las cookies de sesión que genere su servidor de aplicaciones deben incluir el atributo <code>HttpOnly</code>. Por ejemplo, al usar el servidor de aplicaciones JBoss, puede establecer el elemento SessionCookie en <code>httpOnly="true"</code> en el archivo <code>WEB-INF/web.xml</code>.</p> <p>Puede restringir el envío de cookies para que se envían únicamente a través de HTTPS. Como resultado, las cookies no se enviarán sin cifrar a través de HTTP. Los administradores del servidor de aplicaciones deben habilitar las cookies seguras en el servidor a nivel global. Por ejemplo, al usar el servidor de aplicaciones JBoss, puede establecer el elemento connector en <code>secure=true</code> en el archivo <code>server.xml</code>.</p> <p>Consulte la documentación del servidor de aplicaciones para obtener más información sobre la configuración de las cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Examen de directorios</p> </td> 
   <td><p>Cuando alguien solicita una página que no existe o solicita el nombre de un director (la cadena de solicitud termina con una barra diagonal (/)), el servidor de aplicaciones no debe devolver el contenido de ese directorio. Para evitarlo, puede desactivar el examen de directorios en el servidor de aplicaciones. Debe hacerlo en la aplicación de la consola de administración y en el resto de las aplicaciones que se ejecutan en el servidor.</p> <p>En el caso de JBoss, establezca el valor del parámetro de inicialización listings de la propiedad <code>DefaultServlet</code> en <code>false</code> en el archivo web.xml, como se muestra en este ejemplo:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>En el caso de WebSphere, establezca la propiedad <code>directoryBrowsingEnabled</code> del archivo bm-web-ext.xmi en <code>false</code>.</p> <p>En WebLogic, establezca las propiedades de los directorios del índice del archivo weblogic.xml en <code>false</code>, como se muestra en este ejemplo:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Seguridad de la base de datos {#database-security}

A la hora de proteger la base de datos, debe implementar las medidas descritas por el proveedor de esta. Debe asignar un usuario de base de datos con el mínimo de permisos de base de datos requeridos otorgados para su uso por AEM Forms en JEE. Por ejemplo, no utilice una cuenta con privilegios de administrador de base de datos.

En Oracle, la cuenta de la base de datos utilizada solo necesita los privilegios CONNECT, RESOURCE y CREATE VIEW. Para ver requisitos similares de otras bases de datos, consulte [Preparación para instalar AEM Forms en JEE (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_es).

#### Configuración de la seguridad integrada de SQL Server en Windows para JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifique [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} para agregar `integratedSecurity=true` a la URL de conexión, como se muestra en este ejemplo:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Agregue el archivo sqljdbc_auth.dll a la ruta del sistema de Windows en el equipo que ejecuta el servidor de aplicaciones. El archivo sqljdbc_auth.dll se encuentra con la instalación del controlador Microsoft SQL JDBC 6.2.1.0.
1. Modifique la propiedad del servicio de Windows de JBoss (JBoss para AEM Forms en JEE) para Iniciar sesión desde el sistema local en una cuenta de inicio de sesión que tenga una base de datos de AEM Forms y un conjunto mínimo de privilegios. Si está ejecutando JBoss desde la línea de comandos en lugar de como un servicio de Windows, no necesita realizar este paso.
1. Cambie la seguridad de SQL Server del modo **Mixto** a **Solo autenticación de Windows**.

#### Configuración de la seguridad integrada de SQL Server en Windows para WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Inicie la consola de administración del servidor de WebLogic escribiendo la siguiente URL en la línea URL de un explorador web:

   ```java
   https://[host name]:7001/console
   ```

1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura de dominio, haga clic en *[base_domain]* > **Servicios** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **IDP_DS**.
1. En la siguiente pantalla, en la pestaña **Configuración**, haga clic en la pestaña **Grupo de conexiones** y, en el cuadro **Propiedades**, escriba `integratedSecurity=true`.
1. En Estructura de dominio, haga clic en **[base_domain]** > **Servicios** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **RM_DS**.
1. En la siguiente pantalla, en la pestaña **Configuración**, haga clic en la pestaña **Grupo de conexiones** y, en el cuadro **Propiedades**, escriba `integratedSecurity=true`.
1. Agregue el archivo sqljdbc_auth.dll a la ruta del sistema de Windows en el equipo que ejecuta el servidor de aplicaciones. El archivo sqljdbc_auth.dll se encuentra con la instalación del controlador Microsoft SQL JDBC 6.2.1.0.
1. Cambie la seguridad de SQL Server del modo **Mixto** a **Solo autenticación de Windows**.

#### Configuración de la seguridad integrada de SQL Server en Windows para WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

En WebSphere, solo puede configurar la seguridad integrada cuando utiliza un controlador JDBC de SQL Server externo, no el controlador JDBC de SQL Server incrustado en WebSphere.

1. Inicie sesión en la Consola administrativa de WebSphere.
1. En el árbol de navegación, haga clic en **Recursos** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **IDP_DS**.
1. En el panel derecho, en Propiedades adicionales, haga clic en **Propiedades personalizadas** y, a continuación, haga clic en **Nuevo**.
1. En el cuadro **Nombre**, escriba `integratedSecurity` y, en el cuadro **Valor**, escriba `true`.
1. En el árbol de navegación, haga clic en **Recursos** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **RM_DS**.
1. En el panel derecho, en Propiedades adicionales, haga clic en **Propiedades personalizadas** y, a continuación, haga clic en **Nuevo**.
1. En el cuadro **Nombre**, escriba `integratedSecurity` y, en el cuadro **Valor**, escriba `true`.
1. En el equipo en el que está instalado WebSphere, agregue el archivo sqljdbc_auth.dll a la ruta del sistema de Windows (C:\Windows). El archivo sqljdbc_auth.dll se encuentra en la misma ubicación que la instalación del controlador Microsoft SQL JDBC 1.2 (el valor predeterminado es *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Seleccione **Inicio** > **Panel de control** > **Servicios**, haga clic con el botón derecho en el servicio de Windows para WebSphere (Servidor de aplicaciones IBM WebSphere &lt;version> - &lt;node>) y seleccione **Propiedades**.
1. En el cuadro de diálogo Propiedades, haga clic en la pestaña **Iniciar sesión**.
1. Seleccione **Esta cuenta** y proporcione la información necesaria para configurar la cuenta de inicio de sesión que desea utilizar.
1. Cambie la seguridad de SQL Server del modo **Mixto** a **Solo autenticación de Windows**.

### Protección del acceso al contenido confidencial en la base de datos {#protecting-access-to-sensitive-content-in-the-database}

El esquema de la base de datos de AEM Forms contiene información confidencial sobre la configuración del sistema y los procesos empresariales, y debe ocultarse detrás del cortafuegos. La base de datos debe considerarse dentro del mismo límite de confianza que Forms Server. Para evitar la divulgación de información y el robo de datos empresariales, el administrador de la base de datos (DBA) debe configurar la base de datos para permitir el acceso únicamente a los administradores autorizados.

Como precaución adicional, debe considerar la posibilidad de utilizar las herramientas específicas del proveedor de bases de datos para cifrar columnas en las tablas que contienen los siguientes datos:

* Claves de documento de Rights Management
* Clave de cifrado del PIN de HSM del almacén de confianza
* Hashes de contraseña de usuario local

Para obtener información sobre las herramientas específicas del proveedor, consulte [&quot;Información de seguridad de la base de datos&quot;](https://helpx.adobe.com/es/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Seguridad LDAP {#ldap-security}

AEM Forms utiliza normalmente un directorio de protocolo ligero de acceso a directorios (LDAP) en JEE como fuente de información de los usuarios y los grupos empresariales, y como medio para realizar la autenticación de contraseñas. Debe asegurarse de que el directorio LDAP esté configurado para utilizar la capa de sockets seguros (SSL) y de que AEM Forms en JEE está configurado para acceder al directorio LDAP a través del puerto SSL.

#### Denegación de servicio LDAP {#ldap-denial-of-service}

Normalmente, cuando se lleva a cabo un ataque mediante LDAP, el atacante realiza varios intentos de autenticación fallidos de forma deliberada. Esto obliga al servidor de directorio LDAP a bloquear a un usuario en todos los servicios que dependen de LDAP.

Puede establecer el número de intentos erróneos y el periodo de bloqueo posterior que implementa AEM Forms cuando un usuario no se autentica correctamente de forma repetida. En la consola de administración, seleccione valores reducidos. Al seleccionar el número de intentos erróneos, es importante tener en cuenta que, una vez se llevan a cabo todos los intentos, AEM Forms bloquea al usuario antes de que lo haga el servidor del directorio LDAP.

#### Establecer el bloqueo automático de cuentas {#set-automatic-account-locking}

1. Inicie sesión en la consola de administración.
1. Haga clic en **Configuración** > **User Management** > **Administración de dominios**.
1. En Configuración del bloqueo automático de cuentas, establezca **Máximo de errores de autenticación consecutivos** en un número bajo; por ejemplo, 3.
1. Haga clic en **Guardar**.

### Auditoría y registro {#auditing-and-logging}

El uso adecuado y seguro de la auditoría y el registro de aplicaciones puede ayudarle a garantizar que se detecta y se realiza un seguimiento de los eventos de seguridad y de otros eventos anómalos lo antes posible. El uso efectivo de la auditoría y el registro dentro de una aplicación incluye elementos como el seguimiento de inicios de sesión correctos y fallidos, y eventos clave de la aplicación como la creación o eliminación de registros clave.

Puede utilizar la auditoría para detectar numerosos tipos de ataques, incluidos los siguientes:

* Ataques de contraseña por fuerza bruta
* Ataques de denegación de servicio
* Inserción de entradas hostiles y clases relacionadas de ataques de script

En esta tabla se describen las técnicas de auditoría y registro que puede utilizar para reducir las vulnerabilidades del servidor.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ACL de archivos de registro</p> </td> 
   <td><p>Establezca las listas de control de acceso (ACL) de los archivos de registro de AEM Forms en JEE apropiadas.</p> <p>La configuración de las credenciales adecuadas contribuye a evitar que los atacantes eliminen los archivos.</p> <p>Los permisos de seguridad del directorio de los archivos de registro deben ser Control total para los grupos Administradores y SYSTEM. La cuenta de usuario de AEM Forms solo debe tener permisos de lectura y escritura.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redundancia de los archivos de registro</p> </td> 
   <td><p>Si los recursos lo permiten, envíe registros a otro servidor en tiempo real al que el atacante (solo escritura) no pueda acceder mediante Syslog, Tivoli, Microsoft Operations Manager Server (MOM) o cualquier otro mecanismo.</p> <p>Proteger los registros de esta forma contribuye a evitar su manipulación. Además, el almacenamiento de registros en un repositorio central facilita la correlación y la monitorización (por ejemplo, si se utilizan varios servidores de Forms y se está realizando un ataque de averiguación de contraseña en varios equipos en los que se solicita una contraseña para cada equipo).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Permitir que un usuario que no es administrador pueda ejecutar PDF Generator

Puede permitir a un usuario que no sea administrador que utilice PDF Generator. Normalmente, solo los usuarios con privilegios administrativos pueden utilizar PDF Generator. Realice los siguientes pasos para permitir que un usuario que no es administrador ejecute PDF Generator:

1. Cree el nombre de variable de entorno PDFG_NON_ADMIN_ENABLED.

1. Establezca el valor de la variable en TRUE.

1. Reinicie la instancia de AEM Forms.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

## Configuración de AEM Forms en JEE para acceder a la aplicación desde fuera de la empresa {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Después de instalar correctamente AEM Forms en JEE, es importante mantener la seguridad de su entorno de forma periódica. Esta sección describe las tareas recomendadas para mantener la seguridad del servidor de producción de AEM Forms en JEE.

### Configuración de un proxy inverso para el acceso web {#setting-up-a-reverse-proxy-for-web-access}

Puede usar un *proxy inverso* para asegurarse de que un conjunto de URL de aplicaciones web de AEM Forms en JEE está disponible para los usuarios externos e internos. Esta configuración es más segura que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta AEM Forms en JEE. El proxy inverso realiza todas las peticiones HTTP del servidor de aplicaciones que ejecuta AEM Forms en JEE. Los usuarios solo tienen acceso a la red desde el proxy inverso y solo pueden intentar conexiones URL compatibles con el proxy inverso.

**URL raíz de AEM Forms en JEE para su uso con el servidor del proxy inverso**

Las siguientes son las URL raíz de cada aplicación web de AEM Forms en JEE. Debe configurar el proxy inverso para exponer únicamente las URL de la funcionalidad de aplicación web que desea proporcionar a los usuarios finales.

Ciertas URL se resaltan como aplicaciones web dirigidas al usuario final. Debe evitar exponer otras URL del Administrador de configuración para acceder a usuarios externos a través del proxy inverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL raíz</p> </th> 
   <th><p>Finalidad o aplicación web asociada</p> </th> 
   <th><p>Interfaz basada en web</p> </th> 
   <th><p>Acceso del usuario final</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Aplicación web de extensiones de Acrobat Reader DC para aplicar derechos de uso a documentos PDF dirigida a usuario finales</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Aplicación web de Rights Management dirigida a usuarios finales</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL del servicio web de Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>Aplicación web de administración de PDF Generator</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>Aplicación web de Workspace dirigida a usuarios finales</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets y servicios de datos de Workspace requeridos por la aplicación cliente de Workspace</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet para arrancar el repositorio de AEM Forms en JEE</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Página de información de los servicios web de Forms Server</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL del servicio web de todos los servicios de Forms Server</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Aplicación web de administración de Rights Management</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Página de inicio de la consola de administración</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>secured/*</p> </td> 
   <td><p>Páginas de administración de Administración de almacenes de confianza</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Aplicación IVS de Forms para probar y depurar la representación de formularios</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Aplicación IVS de salida para probar y depurar el servicio Output</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL de REST para Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Páginas de administración de Output</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Archivos de la aplicación web de Forms</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Se utiliza para recuperar JavaScript durante la transformación de HTML</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Páginas de administración de Forms</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL de acceso a WebDAV (depuración)</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interfaz de usuario de aplicaciones y servicios</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Páginas de administración de Workspace</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Páginas de soporte de REST</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Página de las opciones de la configuración principal de AEM Forms en JEE</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticación de User Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interfaz de administración de User Management</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>Carga y descarga de documentos que se van a procesar al acceder a puntos de conexión remotos, puntos de conexión WSDL de SOAP y el SDK de Java a través del transporte SOAP o el transporte EJB con documentos HTTP habilitado.</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protección frente a ataques de falsificación de solicitud en sitios múltiples {#protecting-from-cross-site-request-forgery-attacks}

Un ataque de falsificación de solicitud en sitios múltiples (CSRF) explota la confianza que un sitio web tiene en un usuario para transmitir comandos que no han sido autorizados ni enviados intencionadamente por este. El ataque se configura incluyendo un vínculo o un script en una página web o una URL en un mensaje de correo electrónico para acceder a otro sitio en el que el usuario ya se ha autenticado.

Por ejemplo, puede iniciar sesión en la consola de administración mientras navega por otro sitio web. Una de las páginas web puede incluir una etiqueta de imagen HTML con un atributo `src` que identifica un script del lado del servidor en el sitio web atacado. Al utilizar el mecanismo de autenticación de sesión basado en cookies que proporcionan los exploradores web, el sitio web atacante puede enviar solicitudes malintencionadas al script del lado del servidor atacado haciéndose pasar por el usuario legítimo. Para ver más ejemplos, consulte [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

Las siguientes características son comunes al CSRF:

* Incluir sitios que dependen de la identidad de un usuario
* Explotar la confianza del sitio en esa identidad
* Engañar al explorador del usuario para enviar solicitudes HTTP a un sitio de destino
* Incluir solicitudes HTTP con efectos secundarios

AEM Forms en JEE utiliza la función Filtro de referente para bloquear los ataques de CSRF. En esta sección se utilizan los siguientes términos para describir el mecanismo de filtrado de referentes:

* **Referente permitido:** un referente es la dirección de la página de origen que envía una solicitud al servidor. En el caso de las páginas o formularios JSP, el referente suele ser la página anterior del historial de exploración. El referente de las imágenes suele ser la página en la que se muestran. Puede identificar los referentes a los que se permite acceder a los recursos del servidor agregándolos a la lista Referentes permitidos.
* **Excepciones de referentes permitidos:** es posible que desee restringir el ámbito de acceso de un referente en concreto de la lista Referentes permitidos. Para aplicar esta restricción, puede agregar las rutas individuales de ese referente a la lista Excepciones de referentes permitidos. Las solicitudes procedentes de las rutas incluidas en la lista Excepciones de referentes permitidos no pueden invocar ningún recurso del servidor de Forms. Puede definir Excepciones de referentes permitidos para una aplicación específica, y también utilizar una lista global de excepciones que se aplicarán a todas las aplicaciones.
* **URI permitidos:** se trata de una lista de recursos que se deben proporcionar sin marcar el encabezado Referente. A esta lista se pueden agregar los recursos —por ejemplo, páginas de ayuda— que no producen cambios de estado en el servidor. El Filtro de referente nunca bloquea los recursos de la lista URI permitidos independientemente de quién sea el referente.
* **Referente nulo:** una solicitud de servidor que no esté asociada a una página web principal o que no se origine a partir de ella se considera una solicitud de un referente nulo. Por ejemplo, al abrir una nueva ventana del explorador, escribir una dirección y pulsar Intro, el referente enviado al servidor es nulo. Una aplicación de escritorio (.NET o SWING) que realiza una solicitud HTTP a un servidor web, también envía un referente nulo al servidor.

### Filtrado de referentes {#referer-filtering}

El proceso de filtrado de referentes se puede describir de la siguiente manera:

1. El servidor de Forms comprueba el método HTTP utilizado para la invocación:

   1. Si es POST, el servidor de Forms realiza la comprobación del encabezado Referente.
   1. Si es GET, el servidor de Forms omite la comprobación del referente, a menos que *CSRF_CHECK_GETS* esté establecido en true, en cuyo caso realiza la comprobación del encabezado Referente. *CSRF_CHECK_GETS* se especifica en el archivo *web.xml* de la aplicación.

1. El servidor de Forms comprueba si el URI solicitado existe en la lista de permitidos:

   1. Si el URI está incluido en la lista de permitidos, el servidor acepta la solicitud.
   1. Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el referente de la solicitud.

1. Si hay un referente en la solicitud, el servidor comprueba si es un referente permitido. Si está permitido, el servidor comprueba la existencia de una excepción relacionada con ese referente:

   1. Si existe una excepción, la solicitud se bloquea.
   1. Si hay ninguna excepción, se pasa la solicitud.

1. Si no hay ningún referente en la solicitud, el servidor comprueba si se permite un referente nulo:

   1. Si se permite un referente nulo, se pasa la solicitud.
   1. Si no se permite un referente nulo, el servidor comprueba si el URI solicitado es una excepción para el referente nulo y gestiona la solicitud en consecuencia.

### Administración del filtrado de referentes {#managing-referer-filtering}

AEM Forms en JEE proporciona el Filtro de referente para especificar los referentes a los que se permite el acceso a los recursos del servidor. De manera predeterminada, el Filtro de referente no filtra las solicitudes que utilizan un método HTTP seguro, por ejemplo, GET, a menos que *CSRF_CHECK_GETS* esté establecido en true. Si el número de puerto de una entrada de referente permitida está establecido en 0, AEM Forms en JEE permitirá todas las solicitudes con referente procedentes de ese host independientemente del número de puerto. Si no se especifica ningún número de puerto, solo se permiten las solicitudes del puerto predeterminado 80 (HTTP) o 443 (HTTPS). El Filtro de referente se desactiva si se eliminan todas las entradas de la lista Referentes permitidos.

Cuando instala Document Services por primera vez, la lista Referentes permitidos se actualiza con la dirección del servidor en el que se ha instalado este. Las entradas del servidor incluyen el nombre del servidor, la dirección IPv4, la dirección IPv6 si IPv6 está habilitado, la dirección de bucle invertido y una entrada localhost. El sistema operativo del host devuelve los nombres agregados a la lista Referentes permitidos. Por ejemplo, un servidor con una dirección IP de 10.40.54.187 incluirá las siguientes entradas: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. La lista de permitidos no se actualiza para los nombres no autorizados devueltos por el sistema operativo del host (nombres que no tienen una dirección IPv4, una dirección IPv6 o un nombre de dominio autorizado). Modifique la lista Referente permitidos para adaptarla a su entorno empresarial. No implemente el servidor de Forms en el entorno de producción con la lista Referentes permitidos predeterminada. Si ha modificado cualquiera de los referentes permitidos, las excepciones de los referentes permitidos o los URI, asegúrese de reiniciar el servidor para que los cambios surtan efecto.

**Administración de la lista Referentes permitidos**

Puede administrar la lista Referente permitidos desde la interfaz de User Management en la consola de administración. La interfaz de User Management proporciona la funcionalidad para crear, editar o eliminar la lista. Consulte la sección * [Prevención de ataques CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* de la *ayuda de Administración* para obtener más información sobre cómo trabajar con la lista Referentes permitidos.

**Administración de las listas Excepciones de referentes permitidos y URI permitidos**

AEM Forms en JEE proporciona API para administrar las listas Excepciones de referentes permitidos y URI permitidos. Puede utilizar estas API para recuperar, crear, editar o eliminar cada lista. A continuación se muestra una lista de las API disponibles:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Consulte la *Referencia de las API de AEM Forms en JEE* para obtener más información sobre las API.

Utilice la lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** para las excepciones de referentes permitidos a nivel global, es decir, para definir excepciones aplicables a todas las aplicaciones. Esta lista contiene únicamente URI con una ruta de acceso absoluta (por ejemplo, `/index.html`) o relativa (por ejemplo, `/sample/`). También puede anexar una expresión regular al final de un URI relativo, por ejemplo, `/sample/(.)*`.

EL ID de lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** se define como una constante en la clase `UMConstants` del área de nombres `com.adobe.idp.um.api`, que se encuentra en `adobe-usermanager-client.jar`. Puede utilizar las API de AEM Forms para crear, modificar o editar esta lista. Por ejemplo, para crear la lista de excepciones de referentes permitidos globales, utilice:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilice la lista ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** para las excepciones específicas de las aplicaciones.

**Desactivación del Filtro de referente**

En el caso de que el Filtro de referente bloquee por completo el acceso al servidor de Forms y no pueda editar la lista Referentes permitidos, puede actualizar el script de inicio del servidor y deshabilitar el filtrado de referentes.

Incluya el argumento JAVA `-Dlc.um.csrffilter.disabled=true` en el script de inicio y reinicie el servidor. Asegúrese de eliminar el argumento JAVA después de volver a configurar correctamente la lista Referentes permitidos.

**Filtrado de referentes para archivos WAR personalizados**

Es posible que haya creado archivos WAR personalizados para trabajar con AEM Forms en JEE y satisfacer así sus necesidades empresariales. Para habilitar el filtrado de referentes para los archivos WAR personalizados, incluya ***adobe-usermanager-client.jar*** en la ruta de clase del archivo WAR y agregue una entrada de filtro en el archivo *web.xml* con los siguientes parámetros:

**CSRF_CHECK_GETS** controla la comprobación del referente en las peticiones GET. Si no se define este parámetro, el valor predeterminado se establece en False. Incluya este parámetro únicamente si desea filtrar las peticiones GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** es el ID de la lista Excepciones de referentes permitidos. El Filtro de referente evita que las solicitudes procedentes de referentes de la lista identificada por el ID de lista invoquen cualquier recurso del servidor de Forms.

**CSRF_ALLOWED_URIS_LIST_NAME** es el ID de la lista URI permitidos. El Filtro de referente no bloquea las solicitudes de ninguno de los recursos de la lista identificados por el ID de lista, independientemente del valor del encabezado Referente de la solicitud.

**CSRF_ALLOW_NULL_REFERER** controla el comportamiento del Filtro de referente cuando el referente es nulo o no está presente. Si no se define este parámetro, el valor predeterminado se establece en False. Incluya este parámetro únicamente si desea permitir referentes nulos. Permitir referentes nulos puede permitir algunos tipos de ataques de falsificación de solicitud en sitios múltiples.

**CSRF_NULL_REFERER_EXCEPTIONS** es una lista de los URI para los que no se realiza la comprobación del referente cuando el referente es nulo. Este parámetro solo está habilitado cuando *CSRF_ALLOW_NULL_REFERER* se está establecido en False. Separe los diferentes URI de la lista con comas.

A continuación, se muestra un ejemplo de la entrada de filtro del archivo *web.xml* de un archivo WAR ***de ejemplo***:

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**Solución de problemas**

Si el filtro CSRF bloquea las solicitudes legítimas del servidor, pruebe uno de los siguientes métodos:

* Si la solicitud rechazada incluye el encabezado Referente, considere detenidamente la posibilidad de agregarla a la lista Referentes permitidos. Agregue únicamente aquellos referentes en los que confíe.
* Si la solicitud rechazada no incluye el encabezado Referente, modifique la aplicación cliente para incluir este encabezado.
* Si el cliente puede trabajar en un explorador, pruebe ese modelo de implementación.
* Como último recurso, puede agregar el recurso a la lista URI permitidos. No se recomienda esta configuración.

## Configuración de red segura {#secure-network-configuration}

Esta sección describe los protocolos y los puertos requeridos por AEM Forms en JEE y proporciona una serie de recomendaciones para implementar AEM Forms en JEE en una configuración de red segura.

### Protocolos de red utilizados por AEM Forms en JEE {#network-protocols-used-by-aem-forms-on-jee}

Al configurar una arquitectura de red segura como se describe en la sección anterior, son necesarios los siguientes protocolos de red para la interacción entre AEM Forms en JEE y otros sistemas de la red empresarial.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocolo</p> </th> 
   <th><p>Uso</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>El explorador muestra las aplicaciones web del Administrador de configuración y de los usuarios finales</p> </li> 
     <li><p>Todas las conexiones de SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Aplicaciones cliente de los servicios web; p. ej., aplicaciones .NET</p> </li> 
     <li><p>Adobe Reader® utiliza SOAP para los servicios web del servidor de AEM Forms en JEE</p> </li> 
     <li><p>Las aplicaciones Flash® de Adobe utilizan SOAP para los servicios web de Forms Server</p> </li> 
     <li><p>Llamadas del SDK de AEM Forms en JEE cuando se utiliza en el modo SOAP</p> </li> 
     <li><p>Entorno de diseño de Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Llamadas del SDK de AEM Forms en JEE cuando se utiliza en el modo Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrada a un servicio basada en correo electrónico (extremo de correo electrónico)</p> </li> 
     <li><p>Notificaciones de tareas de usuario por correo electrónico</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>IO de archivos UNC</p> </td> 
   <td><p>Monitorización de carpetas inspeccionadas de AEM Forms en JEE para la entrada a un servicio (extremo de carpeta inspeccionada)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizaciones de información de grupos y usuarios de la organización en un directorio</p> </li> 
     <li><p>Autenticación LDAP para usuarios interactivos</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Consultas y llamadas de procedimiento realizadas a una base de datos externa durante la ejecución de un proceso mediante el servicio JDBC</p> </li> 
     <li><p>Acceso interno al repositorio de AEM Forms en JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permite la exploración remota del repositorio de AEM Forms en JEE en tiempo de diseño (formularios, fragmentos, etc.) por cualquier cliente de WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Aplicaciones Flash de Adobe en las que los servicios del servidor de AEM Forms en JEE están configurados con un extremo de Remoting</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms en JEE expone MBeans para la monitorización mediante JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Puertos para servidores de aplicaciones {#ports-for-application-servers}

Esta sección describe los puertos predeterminados (y los intervalos de configuración alternativos) para cada tipo de servidor de aplicaciones compatible. Estos puertos deben habilitarse o deshabilitarse en el cortafuegos interno, según la funcionalidad de red que desee permitir para los clientes que se conectan al servidor de aplicaciones que ejecuta AEM Forms en JEE.

>[!NOTE]
>
>De forma predeterminada, el servidor expone varios MBeans de JMX en el área de nombres de adobe.com. Solo se expone la información que resulta útil para la monitorización del estado del servidor. Sin embargo, para evitar la divulgación de información, debe evitar que los llamadores de una red que no es de confianza busquen los MBeans de JMX y accedan a las métricas de estado.

**Puerto de JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Función</p> </th> 
   <th><p>Puerto </p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acceso a aplicaciones web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Puerto del conector HTTP/1.1 8080</p> <p>Puerto 8009 del conector AJP 1.3</p> <p>Puerto del conector SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Compatibilidad con CORBA</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Puertos de WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Función</p> </th> 
   <th><p>Puerto </p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acceso a aplicaciones web</p> </td> 
   <td> 
    <ul> 
     <li><p>Puerto de escucha del servidor de administración: el valor predeterminado es 7001</p> </li> 
     <li><p>Puerto de escucha SSL del servidor de administración: el valor predeterminado es 7002</p> </li> 
     <li><p>Puerto configurado para el servidor administrado; por ejemplo, 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Los puertos de administración de WebLogic no son necesarios para acceder a AEM Forms en JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Puerto de escucha del servidor administrado: configurable de 1 a 65534</p> </li> 
     <li><p>Puerto de escucha SSL del servidor administrado: configurable de 1 a 65534</p> </li> 
     <li><p>Puerto de escucha del administrador de nodos: el valor predeterminado es 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Puertos de WebSphere**

Para obtener información sobre los puertos de WebSphere que requiere AEM Forms en JEE, vaya a la opción Número de puerto en la interfaz de usuario del servidor de aplicaciones de WebSphere.

### Configurar SSL {#configuring-ssl}

En referencia a la arquitectura física que se describe en la sección [Arquitectura física de AEM Forms en JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), debe configurar SSL para todas las conexiones que planea usar. Específicamente, todas las conexiones de SOAP deben realizarse a través de SSL para evitar la exposición de las credenciales de usuario en una red.

Para obtener instrucciones sobre cómo configurar SSL en JBoss, WebLogic y WebSphere, consulte &quot;Configuración de SSL&quot; en la [Ayuda de Administración](https://www.adobe.com/go/learn_aemforms_admin_64_es).

Para obtener instrucciones sobre cómo importar certificados en una JVM (Máquina virtual Java) configurada para un servidor de AEM Forms, consulte la sección Autenticación mutua de la [Ayuda de AEM Forms Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65_es).

### Configuración del redireccionamiento SSL {#configuring-ssl-redirect}

Después de configurar el servidor de aplicaciones para que admita SSL, debe asegurarse de que todo el tráfico HTTP a las aplicaciones y los servicios utiliza obligatoriamente el puerto SSL.

Para configurar el redireccionamiento SSL en WebSphere o WebLogic, consulte la documentación del servidor de aplicaciones.

1. Abra el Símbolo del sistema, vaya al directorio /JBOSS_HOME/standalone/configuration y ejecute el siguiente comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Abra el archivo JBOSS_HOME/standalone/configuration/standalone.xml para editarlo.

   Agregue los siguientes detalles después del elemento &lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Agregue el siguiente código en el elemento https connector:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Guarde y cierre el archivo standalone.xml.

## Recomendaciones de seguridad específicas para Windows {#windows-specific-security-recommendations}

Esta sección contiene recomendaciones de seguridad específicas para Windows cuando se usa para ejecutar AEM Forms en JEE.

### Cuentas del servicio de JBoss {#jboss-service-accounts}

La instalación llave en mano de AEM Forms en JEE configura una cuenta de servicio de forma predeterminada mediante la cuenta del sistema local. La cuenta de usuario integrada del sistema local tiene un alto nivel de accesibilidad y forma parte del grupo Administradores. Si la identidad de un proceso de trabajo se ejecuta como la cuenta de usuario del sistema local, ese proceso de trabajo tiene acceso completo a todo el sistema.

#### Ejecute el servidor de aplicaciones con una cuenta no administrativa {#run-the-application-server-using-a-non-administrative-account}

1. En Microsoft Management Console (MMC), cree un usuario local para que el servicio Forms Server inicie sesión como:

   * Seleccione **El usuario no puede cambiar la contraseña**.
   * En la pestaña **Miembro de**, asegúrese de que el grupo Usuarios aparece en la lista.

1. Seleccione **Configuración** > **Herramientas administrativas** > **Servicios**.
1. Haga doble clic en el servicio del servidor de aplicaciones y deténgalo.
1. En la pestaña **Inicio de sesión**, seleccione **Esta cuenta**, busque la cuenta de usuario que ha creado e introduzca su contraseña.
1. En la ventana Configuración de seguridad local, en Asignación de derechos de usuario, otorgue los siguientes derechos a la cuenta de usuario en la que se ejecuta el servidor de Forms:

   * Denegar el inicio de sesión a través de Terminal Services
   * Denegar el inicio de sesión de forma local
   * Iniciar sesión como servicio (ya debería estar configurado)

1. Asigne a la nueva cuenta de usuario permisos de modificación en los siguientes directorios:
   * **Directorio Global Document Storage (GDS)**: la ubicación del directorio GDS se configura manualmente durante el proceso de instalación de AEM Forms. Si la configuración de la ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones en `[JBoss root]/server/[type]/svcnative/DocumentStorage`.
   * **Directorio CRX-Repository**: la ubicación predeterminada es `[AEM-Forms-installation-location]\crx-repository`.
   * **Directorios temporales de AEM Forms**:
      * (Windows) Ruta TMP o TEMP tal como se establece en las variables de entorno
      * (AIX, Linux o Solaris) Directorio raíz del usuario que ha iniciado sesión
En sistemas basados en UNIX, un usuario no raíz puede utilizar el siguiente directorio como directorio temporal:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Asigne permisos de escritura a la nueva cuenta de usuario en los siguientes directorios:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >La ubicación de instalación predeterminada del servidor de aplicaciones JBoss:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/.

1. Inicie el servicio del servidor de aplicaciones.

### Seguridad del sistema de archivos {#file-system-security}

AEM Forms en JEE utiliza el sistema de archivos de las siguientes formas:

* Almacena los archivos temporales que se utilizan al procesar la entrada y salida del documento
* Almacena archivos en el almacén de archivos global que se utiliza para admitir los componentes de la solución instalados
* Las carpetas inspeccionadas almacenan archivos colocados que se utilizan como entrada en un servicio desde una ubicación de carpetas del sistema de archivos

Cuando utilice carpetas inspeccionadas para enviar y recibir documentos con un servicio de Forms Server, tome precauciones adicionales a la hora de garantizar la seguridad del sistema de archivos. Cuando un usuario coloca contenido en la carpeta inspeccionada, ese contenido se expone a través de la carpeta inspeccionada. En este caso, el servicio no autentica al usuario final real. En su lugar, se basa en la seguridad de nivel ACL y Share que se debe establecer en el nivel de carpeta para determinar quién puede invocar el servicio de forma efectiva.

## Recomendaciones de seguridad específicas para JBoss {#jboss-specific-security-recommendations}

Esta sección contiene recomendaciones sobre la configuración del servidor de aplicaciones específicas para JBoss 7.0.6 cuando se utiliza para ejecutar AEM Forms en JEE.

### Desactivar la consola de administración de JBoss y la consola JMX {#disable-jboss-management-console-and-jmx-console}

El acceso a la consola de administración de JBoss y la consola JMX ya está configurado (la monitorización JMX está deshabilitada) cuando instala AEM Forms en JEE en JBoss mediante el método de instalación llave en mano. Si está utilizando su propio servidor de aplicaciones JBoss, asegúrese de que el acceso a la consola de administración de JBoss y a la consola de monitorización JMX esté protegido. El acceso a la consola de monitorización JMX se establece en el archivo de configuración de JBoss llamado jmx-invoker-service.xml.

### Desactivación del examen de directorios {#disable-directory-browsing}

Después de iniciar sesión en la consola de administración, es posible examinar la lista de directorios de la consola modificando la dirección URL. Por ejemplo, si cambia la URL a una de las siguientes, puede aparecer un listado de directorios:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recomendaciones de seguridad específicas para WebLogic {#weblogic-specific-security-recommendations}

Esta sección contiene recomendaciones sobre la configuración del servidor de aplicaciones para proteger WebLogic 9.1 cuando se ejecuta AEM Forms en JEE.

### Desactivación del examen de directorios {#disable_directory_browsing-1}

Establezca las propiedades de los directorios del índice del archivo weblogic.xml en `false`, como se muestra en este ejemplo:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Habilitar el puerto SSL de WebLogic {#enable-weblogic-ssl-port}

De forma predeterminada, WebLogic no habilita el puerto de escucha SSL predeterminado, 7002. Habilite este puerto en la consola de administración del servidor de WebLogic antes de configurar el SSL.

## Recomendaciones de seguridad específicas para WebSphere {#websphere-specific-security-recommendations}

Esta sección contiene recomendaciones sobre la configuración del servidor de aplicaciones para proteger WebSphere cuando se ejecuta AEM Forms en JEE.

### Desactivación del examen de directorios {#disable_directory_browsing-2}

Establezca la propiedad `directoryBrowsingEnabled` en el archivo ibm-web-ext.xml en `false`.

### Habilitar la seguridad administrativa de WebSphere {#enable-websphere-administrative-security}

1. Inicie sesión en la Consola administrativa de WebSphere.
1. En el árbol de navegación, vaya a **Seguridad** > **Seguridad global**
1. Seleccione **Habilitar la seguridad administrativa**.
1. Anular la selección de las opciones **Habilitar seguridad de la aplicación** y **Usar la seguridad Java 2**.
1. Haga clic en **Aceptar** o **Aplicar**.
1. En el cuadro **Mensajes**, haga clic en **Guardar directamente en la configuración maestra**.
