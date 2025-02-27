---
title: Instalación independiente personalizada
description: Obtenga información sobre las opciones disponibles al instalar una instancia independiente de AEM.
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: ee0a8865faf594253139e89d4e6ea20a1cb27f62
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 0%

---

# Instalación independiente personalizada{#custom-standalone-install}

En esta sección se describen las opciones disponibles al instalar una instancia de AEM independiente. También puede leer [Elementos de almacenamiento](/help/sites-deploying/storage-elements-in-aem-6.md) para obtener más información sobre cómo elegir el tipo de almacenamiento back-end después de instalar AEM 6.

## Cambio del número de puerto al cambiar el nombre del archivo {#changing-the-port-number-by-renaming-the-file}

El puerto predeterminado para AEM es 4502. Si ese puerto no está disponible o ya está en uso, Quickstart se configura automáticamente para usar el primer número de puerto disponible de la siguiente manera: 4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

También puede establecer el número de puerto cambiando el nombre del archivo jar de inicio rápido, de modo que el nombre de archivo incluya el número de puerto; por ejemplo, `cq5-publish-p4503.jar` o `cq5-author-p6754.jar`.

Hay varias reglas que se deben seguir al cambiar el nombre del archivo jar de inicio rápido:

* Cuando cambie el nombre del archivo, debe comenzar por `cq;`, como en `cq5-publish-p4503.jar`.

* Se recomienda que *siempre* agregue al número de puerto el prefijo -p; como en cq5-publish-p4503.jar o cq5-author-p6754.jar.

>[!NOTE]
>
>Esto sirve para asegurarse de que no tiene que preocuparse por cumplir las reglas utilizadas para extraer el número de puerto:
>
>* el número de puerto debe tener 4 o 5 dígitos
>* estos dígitos deben aparecer después de una raya
>* si hay otros dígitos en el nombre de archivo, el número de puerto debe tener el prefijo `-p`
>* se ignora el prefijo &quot;cq5&quot; al principio del nombre de archivo
>

>[!NOTE]
>
>También puede cambiar el número de puerto utilizando la opción `-port` en el comando de inicio.

### Consideraciones sobre Java 17 {#java-considerations}

Si está ejecutando Oracle Java 17, se deben agregar modificadores adicionales a la línea de comandos al iniciar AEM.

A continuación se muestra un ejemplo del aspecto que deberían tener los parámetros de JVM adicionales al iniciar AEM en Java 17:

```shell
-XX:+UseG1GC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED --add-opens=java.base/java.lang=org.apache.sling.commons.threads -Djdk.util.zip.disableZip64ExtraFieldValidation=true
```

## Ejecutar modos {#run-modes}

**Los modos de ejecución** le permiten ajustar la instancia de AEM para un propósito específico; por ejemplo, crear o publicar, probar, desarrollar, intranet, etc. Estos modos también permiten controlar el uso del contenido de muestra. Este contenido de muestra se define antes de que se genere el inicio rápido y puede incluir paquetes, configuraciones, etc. Esto puede resultar especialmente útil para instalaciones listas para la producción cuando desea mantener la instalación limpia y sin contenido de muestra. Para obtener más información, consulte:

* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

## Agregar un proveedor de instalación de archivos {#adding-a-file-install-provider}

De manera predeterminada, la carpeta `crx-quickstart/install` está vigilada en busca de archivos.
Esta carpeta no existe, pero simplemente se puede crear durante la ejecución.

Si se coloca un paquete, configuración o paquete de contenido en este directorio, se recoge e instala automáticamente. Si se quita, se desinstala.
Es otra forma de colocar paquetes, paquetes de contenido o configuraciones en el repositorio.

Esto resulta especialmente interesante para varios casos de uso:

* Durante el desarrollo, podría ser más fácil colocar algo en el sistema de archivos.
* Si algo sale mal, la consola web y el repositorio no están accesibles. Con esto puede colocar paquetes adicionales en este directorio y deberían instalarse.
* La carpeta `crx-quickstart/install` se puede crear antes de iniciar el inicio rápido y se pueden colocar allí paquetes adicionales.

>[!NOTE]
>
>Consulte también [Cómo instalar paquetes de CRX automáticamente al iniciar el servidor](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) para ver ejemplos.

## Instalación e inicio de Adobe Experience Manager as a Windows Service {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>Asegúrese de realizar el siguiente procedimiento mientras está conectado como administrador o inicie o ejecute estos pasos utilizando la selección de menú contextual **Ejecutar como administrador**.
>
>Iniciar sesión como usuario con privilegios de administrador es **insuficiente**. Si no inició sesión como administrador al completar estos pasos, recibirá **errores de acceso denegado**.

Para instalar e iniciar AEM as a Windows Service:

1. Abra el archivo crx-quickstart\opt\helpers\instsrv.bat en un editor de texto.
1. Si está configurando un servidor Windows de 64 bits, reemplace todas las instancias de prunsrv por uno de los siguientes comandos, según el sistema operativo:

   * prunsrv_amd64
   * prunsrv_ia64

   Este comando invoca el script adecuado que inicia el daemon de servicio de Windows en Java de 64 bits en lugar de Java de 32 bits.

1. Abra el Símbolo del sistema, cambie el directorio actual a la carpeta crx-quickstart/opt/helpers de la instalación de AEM e introduzca el siguiente comando para crear el servicio:

   `instsrv.bat cq5`

   Para comprobar que el servicio se ha creado, abra Servicios en el panel de control Herramientas administrativas o escriba `start services.msc` en el símbolo del sistema. El servicio cq5 aparece en la lista.

1. Inicie el servicio realizando una de las siguientes acciones:

   * En el panel de control Servicios, haga clic en cq5 y en Iniciar.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * En la línea de comandos, escriba net start cq5.

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows indica que el servicio se está ejecutando. AEM se inicia y el ejecutable prunsrv aparece en el Administrador de tareas. En el explorador web, vaya a AEM, por ejemplo, `https://localhost:4502` para empezar a usar AEM.

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>Los valores de propiedad del archivo instsrv.bat se utilizan al crear el servicio de Windows. Si edita los valores de las propiedades en instsrv.bat, debe desinstalar y volver a instalar el servicio.

>[!NOTE]
>
>Al instalar AEM como servicio, debe proporcionar la ruta absoluta para el directorio de registros de `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` desde el Administrador de configuración.

Para desinstalar el servicio, haga clic en **Detener** en el panel de control de **Servicios** o en la línea de comandos, vaya a la carpeta y escriba `instsrv.bat -uninstall cq5`. El servicio se quita de la lista del panel de control **Services** o de la lista de la línea de comandos al escribir `net start`.

## Redefinición de la ubicación del directorio de trabajo temporal {#redefining-the-location-of-the-temporary-work-directory}

La ubicación predeterminada de la carpeta temporal de la máquina java es `/tmp`. AEM también utiliza esta carpeta, por ejemplo, al crear paquetes.

Si desea cambiar la ubicación de la carpeta temporal (por ejemplo, si necesita un directorio con más espacio libre), defina un * `<new-tmp-path>`* añadiendo el parámetro JVM:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

para:

* la línea de comandos de inicio del servidor
* el parámetro de entorno CQ_JVM_OPTS en el script de inicio o serverctl

## Más opciones disponibles en el archivo de inicio rápido {#further-options-available-from-the-quickstart-file}

En el archivo de ayuda de inicio rápido, disponible a través de la opción -help, se describen más opciones y convenciones de cambio de nombre. Para acceder a la ayuda de, escriba:

* `java -jar <jar-name>.jar -help`

>[!CAUTION]
>
>Estas opciones son válidas a partir de la versión original de AEM 6.5 LTS. Es posible realizar cambios en versiones posteriores del Service Pack.

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/<jar-name>.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20250226)                            
--------------------------------------------------------------------------------
Usage:                                                                          
 Use these options on the Quickstart command line.                              
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message                                                 
-quickstart.server.port (-p,-port) <port>
         Set server port number                                                 
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path                                                       
-debug <port>
         Enable Java Debugging on port number; forces forking                   
-gui 
         Show GUI if running on a terminal                                      
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup                                         
-unpack
         Unpack installation files only, do not start the server (implies       
         -verbose)                                                              
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin          
-nofork
         Do not fork the JVM, even if not running on a console                  
-fork
         Force forking the JVM if running on a console, using recommended       
         default memory settings for the forked JVM.                            
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m '.     
         Use -- to specify values starting with -, example: '-forkargs --       
         -server'                                                               
-a (--interface) <interface>
         Optional IP address (interface) to bind to                             
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a    
         process                                                                
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)                        
-b <string>
         Base folder - defines the path under which the quickstart work folder  
         is created                                                             
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup    
-use-control-port
         Start a control port                                                   
-nointeractive
         Start with no interactivity                                            
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
-n   
         Do not install shutdown hook                                           
-D<property>=<value>
         Additional framework properties.                                       
-listener-port <listener-port>
         Set listener port number                                               
-x <string>
         Run a Quickstart extension.                                            
  Options for executing Quickstart extensions:
                                                                                
    -xargs <arg> [<arg> ...]
         Construct an arguments list for a Quickstart extension (e.g. -xargs -- 
         -arg1 val1 -arg2 val2).                                                
--------------------------------------------------------------------------------
Quickstart filename options                                                     
--------------------------------------------------------------------------------
Usage:                                                                          
 Rename the jar file, including one of the patterns shown below, to set the     
corresponding option. Command-line options have priority on these filename      
patterns.                                                                       
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port 
         NNNN, for example: quickstart-8085.jar                                 
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the    
         browser at startup, example: quickstart-nobrowser-8085.jar             
-publish
         Include -publish in the renamed jar filename to run in "publish" mode, 
         example: cq-publish-7502.jar                                           
-dynamicmedia
         Include -dynamicmedia in the renamed jar filename to run in            
         "dynamicmedia" mode, example: quickstart-dynamicmedia-4502.jar         
-dynamicmedia_scene7
         Include -dynamicmedia_scene7 in the renamed jar filename to run in     
         "dynamicmedia_scene7" mode, example:                                   
         quickstart-dynamicmedia_scene7-p4502.jar                               
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the    
  licensing form displayed on first startup and stored in the folder from where 
  Quickstart is run.                                                            
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under   
  /Users/Desktop/AEM/crx-quickstart/logs.               
--------------------------------------------------------------------------------
```

## Instalación de AEM en el entorno Amazon EC2 {#installing-aem-in-the-amazon-ec-environment}

Al instalar AEM en una instancia de Amazon Elastic Compute Cloud (EC2), si instala Author y Publish en la instancia EC2, la instancia de Author se instala correctamente siguiendo el procedimiento de [Instalación de instancias de AEM Manager](#installinginstancesofaemmanager); sin embargo, la instancia de Publish se convierte en Author.

Antes de instalar la instancia de publicación en el entorno EC2, haga lo siguiente:

1. Desempaquete el archivo jar para la instancia de publicación antes de iniciar la instancia por primera vez. Para desempaquetar el archivo, utilice el siguiente comando:

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >Si cambia el modo **después de** de iniciar la instancia la primera vez, no podrá cambiar el modo de ejecución.

1. Inicie la instancia ejecutando:

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >Asegúrese de ejecutar primero la instancia después de desempaquetarla ejecutando el comando anterior. De lo contrario, no se generará el relleno quickstart.properties. Sin este archivo, cualquier actualización futura de AEM fallará.

1. En la carpeta **bin**, abra el script **start** y marque la siguiente sección:

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. Cambie el modo de ejecución a **publish** y guarde el archivo.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. Detenga la instancia y reiníciela ejecutando el script **start**.

## Verificación de la instalación {#verifying-the-installation}

Los siguientes vínculos se pueden utilizar para comprobar que la instalación está operativa (todos los ejemplos se basan en que la instancia se está ejecutando en el puerto 8080 del localhost, que CRX está instalado en /crx y Launchpad en /):

* `https://localhost:8080/crx/de`
La consola de CRXDE Lite.

* `https://localhost:8080/system/console`
La consola web.

## Acciones después de la instalación {#actions-after-installation}

Aunque hay muchas posibilidades para configurar AEM WCM, se deben realizar determinadas acciones o al menos revisar inmediatamente después de la instalación:

* Consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para ver las tareas necesarias a fin de asegurarse de que el sistema sigue siendo seguro.
* Revise la lista de usuarios y grupos predeterminados instalados con AEM WCM. Comprueba si deseas realizar acciones en otras cuentas. Consulta [Seguridad y administración de usuarios](/help/sites-administering/security.md) para obtener más información.

## Acceso a CRXDE Lite y la consola web {#accessing-crxde-lite-and-the-web-console}

Una vez iniciado AEM WCM, también puede acceder a:

* [CRXDE Lite](#accessing-crxde-lite): se usa para acceder y administrar el repositorio
* [Consola web](#accessing-the-web-console): se usa para administrar o configurar los paquetes OSGi (también conocida como Consola OSGi)

### Acceso a CRXDE Lite {#accessing-crxde-lite}

Para abrir CRXDE Lite, puedes seleccionar **CRXDE Lite** en la pantalla de bienvenida o usar tu navegador para navegar a

```
 https://<host>:<port>/crx/de/index.jsp
```

Por ejemplo:
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### Acceso a la consola web {#accessing-the-web-console}

Para acceder a la consola web de Adobe CQ, puede seleccionar **Consola OSGi** en la pantalla de bienvenida o usar el explorador para navegar a

```
 https://<host>:<port>/system/console
```

Por ejemplo:
`https://localhost:4502/system/console`
o para la página Paquetes
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

Consulte [Configuración de OSGi con la consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) para obtener más información.

## Desinstalación de Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Como AEM se instala en un solo directorio, no es necesario desinstalar ninguna utilidad. La desinstalación puede ser tan sencilla como eliminar todo el directorio de instalación, aunque la forma de desinstalar AEM depende de lo que desee lograr y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, al eliminar carpetas también se eliminan datos.

>[!NOTE]
>
>Adobe recomienda encarecidamente realizar una copia de seguridad del repositorio antes de eliminar AEM. Si elimina todo el &lt;cq-installation-directory>, eliminará el repositorio. Para conservar los datos del repositorio antes de eliminarlos, mueva o copie la carpeta &lt;cq-installation-directory>/crx-quickstart/repository en otro lugar antes de eliminar las demás carpetas.

Si la instalación de AEM utiliza almacenamiento externo, por ejemplo, un servidor de base de datos, al eliminar la carpeta no se eliminan los datos automáticamente, pero sí la configuración de almacenamiento, lo que dificulta la restauración del contenido JCR.
