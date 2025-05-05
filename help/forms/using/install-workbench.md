---
title: Instalación de Workbench
description: Obtenga información sobre cómo instalar, desinstalar, configurar, administrar o implementar AEM Forms Workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Workbench,Adaptive Forms
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 65%

---

# Instalación de Workbench {#install-workbench}

Este documento contiene instrucciones para instalar y configurar AEM Forms Workbench. El programa de instalación también instala Forms Designer.

## ¿A quién va dirigido este documento? {#who-should-read-this-doc}

Este documento va dirigido a los administradores o los desarrolladores responsables de la instalación, configuración, administración o implementación de Workbench. También se incluye información para configurar el sistema de modo que admita los procesos actualizados de AEM Forms. La información proporcionada se basa en la suposición de que cualquiera que lea este documento está familiarizado con el sistema operativo Microsoft® Windows®.

## Información adicional {#additional-information}

Los recursos de esta tabla pueden ayudarle a obtener más información y a empezar a utilizar AEM Forms.
<table>
 <tbody>
  <tr>
   <td><p><strong>Para obtener información acerca de</strong></p> </td>
   <td><p><strong>Consulte</strong></p> </td>
  </tr>
  <tr>
   <td><p>Información sobre los procedimientos de Workbench</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Ayuda de Workbench</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Información general sobre AEM Forms y su integración con otros productos de Adobe</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65-lts/forms/getting-started/introduction-aem-forms.html?lang=en">Información general sobre AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Toda la documentación disponible para AEM Forms</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65-lts/forms/getting-started/introduction-aem-forms.html?lang=en">Documentación de AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Actualizaciones de parches, notas técnicas e información adicional sobre esta versión del producto</p> </td>
   <td><p>Contacte con el soporte técnico de Adobe Enterprise</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace está en desuso para AEM Forms. Está disponible para la versión de AEM Forms.

## Antes de la instalación {#before-you-install}

### Información general sobre la instalación de Workbench {#workbench-installation-overview}

Workbench es un entorno de desarrollo integrado (IDE) que utilizan los desarrolladores y los autores de formularios para crear formularios y procesos empresariales automatizados. También se utiliza para administrar los recursos y los servicios que utilizan los procesos y los formularios.

La siguiente ilustración muestra la instalación de Workbench, la cual incluye:
* Diseño de procesos con Workbench
* Diseño de formularios con Designer

>[!NOTE]
>
>El servidor de AEM Forms requiere un programa de instalación independiente. Para obtener más información, consulte la documentación de instalación de AEM Forms en JEE.

![representación-de-formulario-predeterminada](assets/installing-workbench.png)

## Requisitos previos del sistema {#system-prerequisites}

Esta sección describe los requisitos de hardware y software y las plataformas compatibles.

### Requisitos mínimos de hardware y software {#minimum-hardware-software-requirements}

**Workbench**
Se recomiendan los siguientes requisitos mínimos:
Espacio en disco para la instalación:
* 680 MB solo para Workbench.
* 2,15 GB en una sola unidad para una instalación completa de Workbench, Designer y el conjunto de muestras.
* 400 MB para directorios de instalación temporales - 200 MB en el directorio \temp de usuario y 200 MB en el directorio temporal de Windows.

>[!NOTE]
>
>Si todas estas ubicaciones residen en una sola unidad, es necesario disponer de 1,5 GB de espacio disponible durante la instalación. Los archivos copiados en los directorios temporales se eliminan cuando finaliza la instalación.

* Requisitos de hardware: Procesador Intel® Pentium® 4 o AMD® equivalente de 1 GHz.
* Java™ Runtime Environment (JRE) 7.0 Actualización 51 o actualizaciones posteriores a la 7.0.
* Resolución de pantalla mínima de 1024 X 768 píxeles o superior con color de 16 bits o superior.
* Conexión de red TCP/IPv4 o TCP/IPv6 al servidor de AEM Forms.
* Instale los paquetes de tiempo de ejecución redistribuibles de Visual C++ 2012 de 32 bits.
* Instale los paquetes de tiempo de ejecución redistribuibles de Visual C++ 2013 de 32 bits.

>[!NOTE]
>
>Debe tener privilegios administrativos para instalar Workbench. Si va a realizar la instalación con una cuenta que no sea de administrador, el instalador le pedirá las credenciales de una cuenta adecuada.

### Plataformas compatibles {#supported-platforms}

Consulte la lista completa de plataformas compatibles con Workbench en [Plataformas compatibles con AEM Forms](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65_es).

## Consideraciones sobre la instalación de Designer {#designer-installation-considerations}

De forma predeterminada, la instalación de Workbench incluye únicamente la versión correspondiente de Designer en inglés. Si la aplicación de instalación de Workbench detecta una versión existente de Designer en el equipo, es posible que la instalación termine y se le pida que elimine la versión actual de Designer para poder continuar.
La siguiente tabla contiene una lista completa de los posibles escenarios de instalación de Designer que puede encontrar y las acciones que debe realizar al instalar Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versión de Designer instalada actualmente</strong></p> </td>
   <td><p><strong>Acciones necesarias</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro o Acrobat Pro Extended (incluye Designer)</p> </td>
   <td><p>Ninguna.<br /> 
La instalación de Workbench detecta una instancia de Designer instalada en el equipo con Acrobat Pro o Acrobat Pro Extended.<br />
En el mismo sistema pueden coexistir distintas versiones de Designer, por ejemplo, Designer 6.4.x para Workbench 6.4 y Designer 6.5.0.x para Workbench 6.5. No es necesario desinstalar la versión de Designer instalada con Acrobat 10 Pro, Acrobat 10 Pro Extended o superior.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (independiente)</p> </td>
   <td><p>Ninguna. <br />La versión de Designer incluida con Workbench solo está disponible en inglés. <br />El instalador de Workbench no reinstala una nueva versión de Designer. En su lugar, se aplica un parche a una versión actualizada integrada en el instalador de Workbench. Esto también le permite utilizar su versión localizada de Designer en Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Desinstalación de Designer (independiente) en Windows 10 {#uninstall-designer-standalone-windows10}

1. Vaya a **Panel de control > Programas > Programas y características**.
1. En la lista Programas actualmente instalados, seleccione **Adobe Designer**.
1. Haga clic en **Desinstalar** y después en **Sí**.

## Instalación de Workbench {#installing-workbench}

Este capítulo describe cómo instalar Workbench.

### Instalación y ejecución de Workbench {#installing-and-running-workbench}

Antes de instalar Workbench, debe asegurarse de que su entorno incluye el software y el hardware necesarios para ejecutarlo (consulte la sección: **Antes de la instalación**).

**Para instalar y ejecutar Workbench:**

1. Realice una de las siguientes tareas:
   * Vaya al directorio \workbench en los medios de instalación y haga doble clic en el archivo run_windows_installer.bat.
   * Descargue y descomprima Workbench en su sistema de archivos. Una vez descargado, vaya al directorio \workbench y haga doble clic en el archivo run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >El programa de instalación de Workbench solo se ejecuta desde una unidad local. No se puede ejecutar desde un sitio remoto.

   >[!NOTE]
   >
   >Si aparece el error &quot;No se pudo crear la máquina virtual Java™&quot;, cree una variable de entorno llamada _JAVA_OPTIONS con valor -Xmx512M y ejecute el programa de instalación.

1. En la pantalla Introducción, haga clic en Siguiente.
1. Lea el Acuerdo de licencia del producto, seleccione Acepto los términos del Acuerdo de licencia y, a continuación, haga clic en Siguiente.
1. (Opcional) Seleccione Instalar Adobe Designer si necesita esta herramienta para crear y modificar formularios.

   >[!NOTE]
   >
   >Puede seguir utilizando la versión de Designer instalada con Acrobat 10 sin seleccionar esta opción.

1. Acepte el directorio predeterminado como se muestra o haga clic en Elegir y vaya al directorio en el que desea instalar Workbench y, a continuación, haga clic en Siguiente.

   >[!NOTE]
   >
   >La ruta del directorio de instalación no debe contener los caracteres # (libras) y $ (dólares).

1. Revise el resumen a la instalación y haga clic en Instalar. El programa de instalación muestra el progreso de la instalación.
1. Revise el resumen de la instalación. Seleccione Iniciar AEM Forms Workbench para poder iniciar Workbench y, a continuación, haga clic en Siguiente.
1. Revise las Notas de la versión y haga clic en Listo.
1. Los siguientes elementos ya están instalados en el equipo:
   * **Workbench**: para ejecutar Workbench desde el menú Inicio, seleccione Todos los programas > AEM Forms > Workbench si decide almacenar la carpeta de acceso directo allí. Para obtener más información, consulte la documentación sobre el <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">uso de Workbench</a>.
   * **Designer**: puede acceder a Designer desde Workbench. Para obtener más información, consulte el tema Introducción en la <a href="https://helpx.adobe.com/content/dam/help/es/experience-manager/6-5/forms/pdf/using-designer.pdf">Ayuda de Designer</a>.
   * **SDK de AEM Forms**: para obtener más información sobre el uso del SDK, consulte <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">Programación con AEM Forms</a>.

## Actualización de procesos {#upgrading-processes}

Los procesos de AEM Forms en JEE se pueden actualizar a aplicaciones de AEM Forms mediante el Asistente de actualización. Consulte Actualización de la documentación de artefactos heredados en la Ayuda de Workbench para obtener más información.

### Configuración e inicio de sesión en un servidor {#configuring-and-logging-server}

Para utilizar Workbench, debe tener una instancia de AEM Forms en ejecución, normalmente en un equipo independiente. Debe tener un nombre de usuario y una contraseña para iniciar sesión en AEM Forms, así como detalles sobre la ubicación del servidor.

>[!NOTE]
>
>Si configuró AEM Forms para utilizar el proveedor de repositorios EMC Documentum® o IBM® FileNet y desea iniciar sesión en un repositorio que no sea el repositorio configurado como predeterminado en la consola de administración de AEM Forms, proporcione el nombre de usuario username@Repository.

### Configuración del tiempo de espera {#configuring-timeout-settings}

De forma predeterminada, el valor del tiempo de espera de Workbench es de dos horas, independientemente de la actividad o la inactividad. Para editar la configuración de tiempo de espera, consulte &quot;Configuración de la administración de usuarios > Configuración de atributos de sistema avanzados&quot; en la <a href="https://experienceleague.adobe.com/docs/experience-manager-65-lts/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">Ayuda de la consola de administración</a>.

### Configurar Workbench para que se conecte a través de HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Para conectar Workbench a un servidor de AEM Forms a través de HTTPS, debe asegurarse de que Workbench reconozca la autoridad de certificación (CA) que emitió la clave pública como de confianza. Si no se reconoce que el certificado proviene de una fuente de confianza, debe actualizar el archivo cacert en el directorio [Workbench_HOME]/workbench/jre/lib/security.

>[!NOTE]
>
>[Workbench_HOME] representa el directorio donde instaló Workbench. La ubicación predeterminada es C:\Program Files (x86)\Adobe Experience Manager forms Workbench.

Asegúrese de conectarse a HTTPS utilizando el nombre especificado en el certificado. Normalmente, este nombre es el nombre de host completo.

**Para actualizar el archivo cacert**:
1. Asegúrese de disponer de una copia del certificado Secure Sockets Layer (SSL). Póngase en contacto con el administrador que configuró el servidor SSL o exporte el certificado utilizando un explorador web.

   >[!NOTE]
   >
   >Para exportar el certificado, abra un explorador web e inicie sesión en la consola de administración. Instale el certificado en el explorador y exporte el certificado desde el explorador a una ubicación de almacenamiento temporal (o directamente al directorio [Workbench_HOME]/workbench/jre/lib/security).

1. Copie el certificado en el directorio [Workbench_HOME]/workbench/jre/lib/security.

1. Abra una ventana del Símbolo del sistema, vaya a [Workbench_HOME]/workbench/jre/bin y luego escriba el siguiente comando:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
donde:
   * `changeit` es la contraseña predeterminada para el almacén de claves cacerts.
   * certname es el certificado seleccionado en el paso 1.
   * Por ejemplo, el alias que elija para el certificado. Este valor se puede cambiar.

1. Cuando se le pida que confíe en el certificado, escriba Yes y pulse la tecla Intro. keytool procede a importar el archivo cacerts en el directorio [Workbench_HOME]/workbench/jre/lib/security.

1. Cierre y reinicie Workbench para aplicar los cambios.

### Configuración de la caché para plantillas generadas dinámicamente {#configuring-cache-settings-for-dynamically-generated-templates}

Los siguientes aspectos de la operación de caché deben tenerse en cuenta si la aplicación genera plantillas únicas sobre la marcha al actualizar automáticamente el contenido XFA. De hecho, cada transacción utiliza una plantilla nueva y única.

Cuando Forms Generator o Output buscan, o actualizan, las entradas en la caché de una plantilla de formulario específica, utilizan varios valores clave para localizar la entrada de caché específica a la que se accede.

* **Nombre del archivo de plantilla**: la ubicación y el nombre de archivo de la plantilla utilizada como identificador único principal del formulario en caché.
* **Marca de tiempo**: el archivo de plantilla contiene una marca de tiempo que se utiliza para determinar la hora a la que el formulario se actualizó por última vez.
* **UUID de plantilla**: Designer inserta en cada plantilla un identificador único (UUID) para el formulario y su versión. Cada vez que se actualiza el formulario, se actualiza el UUID incrustado. Por ejemplo, una plantilla XDP puede mostrar el siguiente contenido:

  `<?xml version="1.0" encoding="UTF-8"?>`
  `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **Opciones de procesamiento**: en la caché de los formularios procesados, el contenido de la caché se almacena de forma independiente para cada conjunto de opciones de procesamiento únicas.


El servicio Forms recibe las plantillas por referencia al nombre de archivo o la ubicación del repositorio, o por valor como objeto XML en la memoria.

* **Plantillas pasadas por referencia**: utiliza la raíz de contenido y el nombre del formulario. Si se pasan plantillas únicas con diferentes nombres de archivo en cada solicitud utilizando este método, la caché del disco crece constantemente y nunca se reutiliza. Para evitarlo, las plantillas únicas deben pasarse con el mismo nombre de archivo para garantizar que se actualice la misma caché para todas las solicitudes.
* **Plantillas transferidas por valor**: utiliza bytes de plantilla pasados junto con los datos mediante el parámetro inDataDoc. Si se pasan plantillas únicas con un UUID diferente mediante este método, la caché del disco crece constantemente y nunca se reutiliza. Para evitarlo, el atributo UUID debe eliminarse de todas las plantillas para garantizar que no se cree ninguna caché para la plantilla. En cambio, pasar el mismo UUID no nulo permite crear los objetos de caché, pero garantiza que se actualice la misma caché con cada solicitud.

Para evitar que la caché crezca indefinidamente, tenga en cuenta los siguientes factores para procesar plantillas generadas dinámicamente con las nuevas API de AEM Forms, que son renderHTMLForm2 y renderPDFForm2.

Al utilizar las nuevas API, la plantilla se pasa como un objeto document, el cual se gestiona en el servicio Forms dependiendo de si está pasivada o no.

Para documentos pasivados en los que el UUID y la raíz de contenido sirven como clave de caché, tenga en cuenta los siguientes aspectos:

* La caché no se crea para plantillas de entrada pasivadas sin UUID.
* Si se pasa más de una plantilla de entrada pasivada que tiene el mismo UUID y la misma raíz de contenido, se sobrescribe la misma caché.

En el caso de los documentos no pasivados en los que el nombre de archivo y la raíz de contenido sirven como clave de caché, tenga en cuenta el siguiente aspecto:

* En el caso de las plantillas de entrada no pasivadas, el almacenamiento en caché depende de la raíz de contenido y del nombre de archivo a partir del cual se generó el documento.
La misma caché solo se utiliza para solicitudes con la misma raíz de contenido y el mismo nombre de archivo de plantilla.
Las siguientes prácticas recomendadas garantizan que la caché no crezca constantemente al pasar plantillas generadas dinámicamente al servicio Forms:
   * Elimine el UUID o pase el mismo UUID en todas las plantillas generadas dinámicamente.
   * Genere el documento desde bytes de plantilla o desde el mismo nombre de archivo en disco.

### Desinstalación de Workbench {#uninstalling-workbench}

Utilice la función Agregar o quitar programas del Panel de control de Campaign para iniciar el programa de desinstalación. Las aplicaciones Workbench y Designer tienen programas de desinstalación independientes.

## Configuración del Editor XDC de AEM Forms {#configuring-aem-forms-xdc-editor}

Con el Editor XDC, los administradores de impresoras de red pueden crear y modificar archivos XML Forms Architecture Device Configuration (XDC). Los archivos XDC describen las capacidades de las impresoras, como el idioma de la impresora o la correlación entre el tamaño del papel y la ubicación de la bandeja.

Antes de que el administrador de la impresora de red utilice el Editor XDC, cambie la ubicación de los archivos XDC de ejemplo y consulte la sección Creación de perfiles de dispositivo mediante el Editor XDC.

**Para obtener los archivos XDC de ejemplo**:

1. En el servidor de AEM Forms, busque la carpeta XDC en [AEM Forms root]\sdk\samples\Output\IVS.
1. Copie el contenido de esta carpeta en un directorio al que se pueda acceder desde el sistema Workbench o Eclipse.

**Para obtener ayuda sobre el Editor XDC**:

1. Vaya al sitio web de documentación de AEM Forms.
1. Haga clic en la pestaña **Desarrollo** y vaya a la sección Creación de perfiles de dispositivo mediante el Editor XDC. Descargue el archivo xdc_editor_help_web.zip e instale los archivos de ayuda siguiendo las instrucciones proporcionadas en el archivo Léame.
