---
title: Instalación y configuración de Document Services
description: Instale AEM Forms Document Services para crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a los documentos y descodificar formularios con código de barras.
topic-tags: installing
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
exl-id: dd22ea1b-33e9-407d-b7b6-645bdba00b4e
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '5660'
ht-degree: 84%

---

# Instalación y configuración de Document Services {#installing-and-configuring-document-services}

AEM Forms proporciona un conjunto de servicios OSGi para realizar distintas operaciones a nivel de documento; por ejemplo, servicios para crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a los documentos y descodificar formularios con código de barras. Estos servicios están incluidos en el paquete de complementos de AEM Forms. El conjunto de estos servicios se denomina Document Services. A continuación, encontrará una lista de los servicios de Document Services disponibles y sus principales capacidades:

* **Servicio Assembler:** permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF. También permite convertir documentos PDF al estándar PDF/A y validarlos, y transformar formularios PDF, formularios XML y formularios PDF a PDF/A-1b, PDF/A-2b y PDFA/A-3b. Para obtener más información, consulte [Servicio Assembler](/help/forms/using/assembler-service.md).

* **Servicio ConvertPDF:** permite convertir documentos PDF en archivos PostScript o archivos de imagen (JPEG, JPEG 2000, PNG y TIFF). Para obtener más información, consulte [Servicio ConvertPDF](/help/forms/using/using-convertpdf-service.md).

* **Servicio de formularios con códigos de barras:** permite extraer datos de imágenes electrónicas de códigos de barras. El servicio acepta archivos TIFF y PDF que incluyen uno o más códigos de barras como entrada y extrae los datos del código de barras. Para obtener más información, consulte [Servicio de formularios con códigos de barras](/help/forms/using/using-barcoded-forms-service.md).

* **Servicio DocAssurance:** permite cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y agregar firmas digitales a los documentos. El servicio Doc Assurance contiene tres servicios: Signature, Encryption y Extensiones de Reader. Para obtener más información, consulte [Servicio DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Servicio Encryption:** permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Para obtener más información, consulte [Servicio Encryption](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servicio Forms:** permite crear aplicaciones cliente de captura de datos interactivas que validen, procesan, transforman y entregan formularios que normalmente se crean en Forms Designer. El servicio Forms procesa cualquier diseño de formulario que hay desarrollado en documentos PDF. Para obtener más información, consulte [Servicio de Forms](/help/forms/using/forms-service.md).

* **Servicio Output:** permite crear documentos en diferentes formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Lenguaje de control de impresora (PCL). Para obtener más información, consulte [Servicio Output](/help/forms/using/output-service.md).

* **Servicio PDF Generator:** el servicio PDF Generator proporciona API para convertir formatos de archivo nativos a PDF. También convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos PDF. Para obtener más información, consulte [Servicio PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servicio Extensiones de Reader:** permite a su organización compartir fácilmente documentos PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio activa funciones que no están disponibles cuando se abre un documento PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Para obtener más información, consulte [Servicio Extensiones de Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servicio Signature:** permite trabajar con firmas digitales y documentos en el servidor de AEM. Por ejemplo, el servicio Signature se suele utilizar en las siguientes situaciones:

   * El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra con Acrobat o Adobe Reader.
   * El servidor de AEM valida una firma que se ha agregado a un formulario mediante Acrobat o Adobe Reader.
   * El servidor de AEM firma un formulario en nombre de un notario público.

  El servicio Signature accede a los certificados y credenciales almacenados en el almacén de confianza. Para obtener más información, consulte [Servicio Signature](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms es una potente plataforma de clase empresarial, y Document Services es solo una de sus capacidades. Para obtener la lista completa de capacidades, consulte [Introducción a AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Por lo general, solo se necesita una instancia de AEM (de autor o publicación) para ejecutar AEM Forms Document Services. Se recomienda la siguiente topología para ejecutar AEM Forms Document Services. Para obtener información detallada sobre topologías, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Arquitectura y topologías de implementación para AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, en el caso de un entorno que utiliza el servicio PDF Generator para convertir miles de páginas al día y varios formularios adaptables para capturar datos, deberá configurar servidores de AEM Forms independientes para el servicio PDF Generator y las capacidades relacionadas con los formularios adaptables. Esto permite proporcionar un rendimiento óptimo y escalar los servidores de forma independiente entre sí.

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar AEM Forms Document Services, asegúrese de lo siguiente:

* Se ha implementado la infraestructura de hardware y software. Para obtener una lista detallada del hardware y el software compatibles, consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo Autor o Publicación. Por lo general, solo necesita una instancia de AEM (Autor o Publicación) para ejecutar AEM Forms Document Services:

   * **Autor**: la instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para su publicación, se replica en la instancia de publicación.
   * **Publicación**: la instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft® Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* Se ha instalado el software cliente requerido para que PDF Generator realice conversiones en Microsoft® Windows y Linux®:

   * **Microsoft® Windows**: instale **Microsoft® Office** o **Apache OpenOffice**.
   * **Linux®**: instale **Apache OpenOffice**.

>[!NOTE]
>
>* En Microsoft® Windows, PDF Generator admite las rutas de conversión WebKit, Acrobat WebCapture y WebToPDF para convertir archivos de HTML en documentos de PDF.
>* En sistemas operativos basados en UNIX, PDF Generator admite las rutas de conversión WebKit y WebToPDF para convertir archivos HTML en documentos PDF.
>

### Requisitos adicionales para sistemas operativos basados en UNIX {#extrarequirements}

Si utiliza un sistema operativo basado en UNIX, instale los siguientes paquetes de 32 bits desde los medios de instalación del sistema operativo correspondiente:
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expat</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(Solo PDF Generator**) Instale la versión de 32 bits de las bibliotecas libcurl, libcrypto y libssl, y cree los siguientes enlaces simbólicos. Los enlaces simbólicos apuntan a la última versión de sus respectivas bibliotecas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(solo PDF Generator)** El servicio PDF Generator admite las rutas WebKit y WebToPDF para convertir archivos HTML en documentos PDF. Para habilitar la conversión para la ruta WebToPDF, instale las bibliotecas de 64 bits que se enumeran a continuación. Por lo general, estas bibliotecas ya están instaladas. Si falta alguna biblioteca, instálela manualmente:

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## Configuraciones previas a la instalación {#preinstallationconfigurations}

Las configuraciones que aparecen en la sección de configuraciones previas a la instalación solo se aplican al servicio PDF Generator. Si no está configurando el servicio PDF Generator, puede omitir la sección Configuración previa a la instalación.

### Instalación de Adobe Acrobat y aplicaciones de terceros {#install-adobe-acrobat-and-third-party-applications}

Si va a usar el servicio PDF Generator para convertir formatos de archivo nativos como Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 y Adobe Acrobat a documentos PDF, asegúrese de que estas aplicaciones estén instaladas en el servidor de AEM Forms.

>[!NOTE]
>
>* Si el servidor de AEM Forms se encuentra en un entorno sin conexión o seguro e Internet no está disponible para activar Adobe Acrobat, consulte [Activación sin conexión](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=es) para obtener instrucciones para activar este tipo de instancias de Adobe Acrobat.
>* Adobe Acrobat, Microsoft® Word, Excel y PowerPoint solo están disponibles para Microsoft® Windows. Si está utilizando el sistema operativo basado en UNIX, instale OpenOffice para convertir archivos de texto enriquecido y archivos compatibles de Microsoft® Office en documentos PDF.
>* Descarte todos los cuadros de diálogo que se muestran después de instalar Adobe Acrobat y el software de terceros en todos los usuarios configurados para utilizar el servicio PDF Generator.
>* Inicie todo el software instalado al menos una vez. Descarte todos los cuadros de diálogo de todos los usuarios configurados para utilizar el servicio PDF Generator.
>* [Compruebe la fecha de caducidad de los números de serie de Adobe Acrobat](https://helpx.adobe.com/es/enterprise/kb/volume-license-expiration-check.html) y establezca una fecha para actualizar la licencia o [migrar su número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) en función de la fecha de caducidad.

Después de instalar Acrobat, abra Microsoft® Word. En la pestaña **Acrobat**, haga clic en **Crear PDF** y convierta un archivo .doc o .docx disponible en su equipo en un documento PDF. Si la conversión se realiza correctamente, AEM Forms está listo para usar Acrobat con el servicio PDF Generator.

### Configuración de variables de entorno {#setup-environment-variables}

Establezca variables de entorno para el kit de desarrollo de Java de 64 bits, las aplicaciones de terceros y Adobe Acrobat. Las variables de entorno deben contener la ruta absoluta del ejecutable utilizado para iniciar la aplicación correspondiente. Por ejemplo, la siguiente tabla siguiente muestra las variables de entorno de algunas aplicaciones:

<table>
 <tbody>
  <tr>
   <td><p><strong>Aplicación</strong></p> </td>
   <td><p><strong>Variable de entorno</strong></p> </td>
   <td><p><strong>Ejemplo</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK (64 bits)</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>Bloc de notas</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Todas las variables de entorno y sus respectivas rutas distinguen entre mayúsculas y minúsculas.
>* JAVA_HOME y Acrobat_PATH (solo Windows) son variables de entorno obligatorias.
>* La variable de entorno OpenOffice_PATH se establece en la carpeta de instalación en lugar de en la ruta del ejecutable.
>* No configure variables de entorno para las aplicaciones de Microsoft® Office, como Word, PowerPoint, Excel y Project, ni para AutoCAD. Si estas aplicaciones están instaladas en el servidor, el servicio Generate PDF las inicia automáticamente.
>* En plataformas basadas en UNIX, instale OpenOffice como /root. Si OpenOffice no está instalado como raíz, el servicio PDF Generator no convierte los documentos de OpenOffice en documentos PDF. Si necesita instalar y ejecutar OpenOffice como un usuario no raíz, proporcione derechos sudo al usuario no raíz.
>* Si está utilizando OpenOffice en una plataforma basada en UNIX, ejecute el siguiente comando para configurar la variable de ruta:
>
>  `export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo para IBM® WebSphere®) Configure el proveedor de sockets SSL de IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Realice los siguientes pasos para configurar el proveedor de sockets SSL de IBM®:

1. Cree una copia del archivo java.security. La ubicación predeterminada del archivo es `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra el archivo java.security copiado para editarlo.
1. Cambie las fábricas de sockets SSL predeterminadas para utilizar las fábricas JSSE2 en lugar de las fábricas IBM® WebSphere® predeterminadas:

   **Contenido predeterminado:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Contenido modificado:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Para permitir que el servidor de AEM Forms use el archivo java.security actualizado, agregue el siguiente argumento Java al iniciar el servidor:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configure las opciones de bloqueo de archivos para Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Cambie la configuración del Centro de confianza de Microsoft® Office para permitir que el servicio PDF Generator convierta archivos creados con versiones anteriores de Microsoft® Office.

1. Abra una aplicación de Microsoft® Office. Por ejemplo, Microsoft® Word. Vaya a **[!UICONTROL Archivo]** > **[!UICONTROL Opciones]**. Aparece el cuadro de diálogo opciones.

1. Haga clic en **[!UICONTROL Centro de confianza]** y, después, en **[!UICONTROL Configuración del Centro de confianza]**.
1. En el **[!UICONTROL Configuración del Centro de confianza]**, haga clic en **[!UICONTROL Configuración de bloqueo de archivos]**.
1. En la lista **[!UICONTROL Tipo de archivo]**, anule la selección de **[!UICONTROL Abrir]** para el tipo de archivo que debe permitirse al servicio PDF Generator convertir archivos en documentos PDF.

### (Solo Windows) Conceder el privilegio Reemplazar un símbolo (token) de nivel de proceso {#grant-the-replace-a-process-level-token-privilege}

La cuenta de usuario utilizada para iniciar el servidor de aplicaciones requiere el privilegio **Reemplazar un token de nivel de proceso**. La cuenta del sistema local tiene el privilegio **Reemplazar un token de nivel de proceso** de forma predeterminada. En los servidores que se ejecutan con un usuario del grupo Administradores locales, el privilegio debe otorgarse explícitamente. Siga estos pasos para conceder el privilegio:

1. Abra el Editor de directivas de grupo de Microsoft® Windows. Para abrir el Editor de directivas de grupo, haga clic en **[!UICONTROL Inicio]**, escriba **gpedit.msc** en el cuadro Iniciar búsqueda y haga clic en **[!UICONTROL Editor de directivas de grupo]**.
1. Vaya a **[!UICONTROL Directiva de equipo local]** > **[!UICONTROL Configuración del equipo]** > **[!UICONTROL Configuración de Windows]** > **[!UICONTROL Configuración de seguridad]** > **[!UICONTROL Directivas locales]** > **[!UICONTROL Asignación de derechos de usuario]** y edite la directiva **[!UICONTROL Reemplazar un símbolo (token) de nivel de proceso]** e incluya el grupo Administradores.
1. Agregue el usuario a la entrada Reemplazar un símbolo (token) de nivel de proceso.

>[!NOTE]
>
> Como se ha insinuado anteriormente, si el servidor de AEM se ejecuta como un servicio en la cuenta LocalSystem (LSA), no es necesario asignar explícitamente este privilegio a un usuario.

### (Solo Windows) Habilite el servicio PDF Generator para usuarios que no sean administradores {#enable-the-pdf-generator-service-for-non-administrators}

Puede habilitar a un usuario que no sea administrador para que utilice el servicio PDF Generator. Normalmente, solo los usuarios con privilegios administrativos pueden utilizar el servicio:

1. Cree una variable de entorno, PDFG_NON_ADMIN_ENABLED.
1. Establezca el valor de la variable de entorno en TRUE.
1. Reinicie la instancia de AEM Forms.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

### (Solo Windows) Deshabilitar el Control de cuentas de usuario (UAC) {#disable-user-account-control-uac}

1. Para acceder a la Utilidad de configuración del sistema, vaya a **[!UICONTROL Inicio > Ejecutar]** y, a continuación, escriba **[!UICONTROL MSCONFIG]**.
1. Haga clic en la pestaña **[!UICONTROL Herramientas]**, desplácese hacia abajo y seleccione **[!UICONTROL Cambiar configuración de UAC]**. Haga clic en **[!UICONTROL Iniciar]** para ejecutar el comando en una nueva ventana.
1. Ajuste el control deslizante al nivel No notificar nunca. Cuando termine, cierre la ventana de comandos y la de Configuración del sistema.
1. Compruebe que la configuración del registro para UAC está establecida en 0 (cero). Siga estos pasos para comprobarlo:

   1. Microsoft® recomienda realizar una copia de seguridad del registro antes de modificarlo. Para ver los pasos detallados, consulte [Realizar una copia de seguridad y restaurar el registro en Windows](https://support.microsoft.com/es-es/help/322756).
   1. Abra el editor del registro de Windows de Microsoft®. Para abrir el editor del registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
   1. Navegue hasta `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Asegúrese de que el valor de EnableLUA está establecido en 0 (cero).
   1. Asegúrese de que el valor de **EnableLUA** esté establecido en 0 (cero). Si el valor no es 0, cambie el valor a 0. Cierre el editor del registro.

1. Reinicie el equipo.

### (Solo Windows) Deshabilitar el servicio Informes de errores {#disable-error-reporting-service}

Al convertir un documento a PDF mediante el servicio PDF Generator en Windows Server, Windows Server informa en algunos casos de que el archivo ejecutable ha encontrado un problema y debe cerrarse. Sin embargo, esto no afecta a la conversión a PDF, ya que continúa en segundo plano.

Para evitar recibir el error, puede deshabilitar los informes de errores de Windows. Para obtener más información sobre cómo deshabilitar los informes de errores, consulte [https://technet.microsoft.com/es-es/library/cc754364.aspx](https://technet.microsoft.com/es-es/library/cc754364.aspx).

### (Solo Windows) Configurar la conversión de HTML a PDF {#configure-html-to-pdf-conversion}

El servicio PDF Generator proporciona rutas o métodos WebKit, WebCapture y WebToPDF para convertir archivos de HTML en documentos de PDF. Para habilitar la conversión mediante las rutas WebKit y Acrobat WebCapture en Windows, copie la fuente Unicode al directorio %windir%\fonts.

>[!NOTE]
>
>Reinicie la instancia de AEM Forms siempre que instale fuentes nuevas en la carpeta de fuentes.

### (Solo plataformas basadas en UNIX) Configuraciones adicionales para la conversión de HTML a PDF  {#extra-configurations-for-html-to-pdf-conversion}

En plataformas basadas en UNIX, el servicio PDF Generator admite las rutas WebKit y WebToPDF para convertir archivos HTML en documentos PDF. Para habilitar la conversión de HTML a PDF, realice las siguientes configuraciones, según la ruta de conversión que prefiera:

### (Solo plataformas basadas en UNIX) Habilitar la compatibilidad con fuentes Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie la fuente Unicode en cualquiera de los siguientes directorios según corresponda para su sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* En Red Hat® Enterprise Linux® 6.x y versiones posteriores, las fuentes Courier no están disponibles. Para instalar las fuentes Courier, descargue el archivo font-ibm-type1-1.0.3.zip. Extraiga el archivo en /usr/share/fonts. Cree un enlace simbólico desde /usr/share/X11/fonts a /usr/share/fonts.
>* Elimine todos los archivos de caché de fuentes .lst de los directorios Html2PdfSvc/bin y /usr/share/fonts.
>* Asegúrese de que los directorios /usr/lib/X11/fonts y /usr/share/fonts existan. Si los directorios no existen, utilice el comando ln para crear un enlace simbólico de /usr/share/X11/fonts a /usr/lib/X11/fonts y otro enlace simbólico de /usr/share/fonts a /usr/share/X11/fonts. Asegúrese también de que las fuentes Courier están disponibles en /usr/lib/X11/fonts.
>* Asegúrese de que todas las fuentes (Unicode y no Unicode) estén disponibles en los directorios /usr/share/fonts o /usr/share/X11/fonts.
>* Cuando ejecute el servicio PDF Generator como usuario no raíz, proporcione a ese usuario acceso de lectura y escritura a todos los directorios de fuentes.
>* Reinicie la instancia de AEM Forms siempre que instale fuentes nuevas en la carpeta de fuentes.
>

## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene AEM Forms Document Services y otras capacidades de AEM Forms. Realice los siguientes pasos para instalar el paquete:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo que aparece en el artículo [Versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere a que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log y el registro sea estable.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

### Configuración de la delegación de arranque para bibliotecas RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Detenga la instancia de AEM. Vaya al [directorio de instalación de AEM]\crx-quickstart\conf\ folder. Abra el archivo sling.properties para editarlo.

   Si usa `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar una instancia de AEM, edite el archivo sling.properties ubicado en `[AEM_root]\crx-quickstart\`.

1. Agregue las siguientes propiedades al archivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Solo AIX®) Agregue las siguientes propiedades al archivo sling.properties:

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Guarde y cierre el archivo.

### Configuración del servicio Administrador de fuentes  {#configuring-the-font-manager-service}

1. Iniciar sesión en el [Administrador de configuración de AEM](http://localhost:4502/system/console/configMgr) como administrador.
1. Busque y abra el servicio **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]**. Especifique la ruta de los directorios de las fuentes del sistema, las fuentes del servidor de Adobe y las fuentes de cliente. Haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Su derecho a utilizar fuentes de terceros distintos de Adobe se rige por los acuerdos de licencia que estos terceros le proporcionen junto con las fuentes, y no está cubierto por la licencia para utilizar el software de Adobe. Adobe recomienda revisar y asegurarse de que cumple todos los acuerdos de licencia aplicables que no sean de Adobe antes de utilizar fuentes que no sean de Adobe con el software de Adobe, especialmente en lo que respecta al uso de fuentes en un entorno de servidor.
   >Cuando instale nuevas fuentes en la carpeta de fuentes, reinicie la instancia de AEM Forms.
   >

### Configuración de una cuenta de usuario local para ejecutar el servicio PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Se necesita una cuenta de usuario local para ejecutar el servicio PDF Generator. Para ver los pasos para crear un usuario local, consulte [Crear una cuenta de usuario en Windows](https://support.microsoft.com/es-es/help/13951/windows-create-user-account) o Crear una cuenta de usuario en plataformas basadas en UNIX.

1. Abra la página [Configuración de AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html).

1. En la pestaña **[!UICONTROL Cuentas de usuario]**, proporcione las credenciales de una cuenta de usuario local y haga clic en **[!UICONTROL Enviar]**. Si Microsoft® Windows se lo solicita, permita el acceso al usuario. Cuando se agrega correctamente, el usuario configurado se muestra en la sección **[!UICONTROL Sus cuentas de usuario]** de la pestaña **[!UICONTROL Cuentas de usuario]**.

### Configuración del tiempo de espera {#configure-the-time-out-settings}

1. En el [Administrador de configuración de AEM](http://localhost:4502/system/console/configMgr), busque y abra el servicio **[!UICONTROL Jacorb ORB Provider]**.

   Agregue lo siguiente en el campo **[!UICONTROL Custom Properties.name]** y haga clic en **[!UICONTROL Guardar]**. Esto establece el tiempo de espera de respuesta pendiente (también conocido como tiempo de espera del cliente CORBA) en 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configuración de PDF Generator]**. La URL predeterminada es <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Abra la **[!UICONTROL Configuración general]** y modifique el valor de los siguientes campos para su entorno:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
   <td>Valor predeterminado</td>
  </tr>
  <tr>
   <td>Tiempo de espera de conversión del servidor</td>
   <td>Una conversión de PDF Generator permanece activa durante el número de segundos definido en el tiempo de espera de conversión del servidor</td>
   <td>270 segundos<br /> </td>
  </tr>
  <tr>
   <td>Segundos de análisis de limpieza de PDF Generator</td>
   <td>El número de segundos necesarios para realizar las operaciones posteriores a la conversión.<br /> </td>
   <td>3600 segundos</td>
  </tr>
  <tr>
   <td>Segundos de caducidad del trabajo</td>
   <td>La duración durante la cual el servicio PDF Generator puede ejecutar una conversión. Asegúrese de que el valor de Segundos de caducidad del trabajo sea mayor que el valor de Segundos del análisis de limpieza de PDF Generator.</td>
   <td>7200 segundos</td>
  </tr>
 </tbody>
</table>

### (Solo Windows) Configurar Acrobat para el servicio PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

En Microsoft® Windows, el servicio PDF Generator utiliza Adobe Acrobat para convertir los formatos de archivo admitidos en un documento PDF. Siga estos pasos para configurar Adobe Acrobat para el servicio PDF Generator:

1. Abra Acrobat y seleccione **[!UICONTROL Editar]** > **[!UICONTROL Preferencias]** > **[!UICONTROL Actualizador]**. En Buscar actualizaciones, anule la selección de **[!UICONTROL Instalar actualizaciones automáticamente]** y haga clic en **[!UICONTROL Aceptar]**. Cierre Acrobat.
1. Haga doble clic en un documento PDF del sistema. Cuando Acrobat se inicia por primera vez, aparecen los cuadros de diálogo Iniciar sesión, Pantalla de bienvenida y EULA. Descarte estos cuadros de diálogo para todos los usuarios configurados para usar PDF Generator.
1. Ejecute el archivo por lotes de la utilidad PDF Generator para configurar Acrobat para el servicio PDF Generator:

   1. Abra el [Administrador de paquetes AEM](http://localhost:4502/crx/packmgr/index.jsp) y descargue el archivo `adobe-aemfd-pdfg-common-pkg-[version].zip` del Administrador de paquetes.
   1. Descomprima el archivo .zip descargado. Abra el Símbolo del sistema con privilegios administrativos.
   1. Vaya a `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. Descomprima `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. Vaya al directorio `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]`. Ejecute el siguiente archivo por lotes:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat está configurado para ejecutarse con el servicio PDF Generator.

1. Ejecute la [Herramienta de preparación del sistema (SRT)](#SRT) para validar la instalación de Acrobat.

### (Solo Windows) Configure la ruta principal para la conversión de HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

El servicio PDF Generator proporciona varias rutas para convertir archivos de HTML en documentos de PDF: Webkit, Acrobat WebCapture (solo Windows) y WebToPDF. Adobe recomienda utilizar la ruta WebToPDF porque tiene la capacidad de gestionar contenido dinámico, no depende de bibliotecas de 32 bits ni requiere fuentes adicionales. Además, la ruta WebToPDF no requiere acceso raíz o sudo para ejecutar la conversión.

La ruta principal predeterminada para la conversión de HTML a PDF es Webkit. Para cambiar la ruta de conversión:

1. En la instancia de autor de AEM, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configuración de PDF Generator]**.

1. En la pestaña **[!UICONTROL Configuración general]**, seleccione la ruta de conversión preferida en la lista desplegable **[!UICONTROL Ruta principal para conversiones de HTML a PDF]**.

### Inicializar el Almacén de confianza global {#intialize-global-trust-store}

Con la administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Realice los siguientes pasos para inicializar un almacén de confianza:

1. Inicie sesión en la instancia de AEM Forms como administrador.
1. Vaya a **[!UICONTROL Herramientas]** >  **[!UICONTROL Seguridad]** >  **[!UICONTROL Almacén de confianza]**.
1. Haga clic en **[!UICONTROL Crear almacén de confianza]**. Establezca la contraseña y seleccione **[!UICONTROL Guardar]**.

### Configuración de certificados para los servicios Encryption y Extensiones de Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

El servicio DocAssurance puede aplicar derechos de uso a los documentos PDF. Para aplicar derechos de uso a documentos PDF, configure los certificados.

Antes de configurar los certificados, asegúrese de que dispone de lo siguiente:

* El archivo del certificado (.pfx).

* La contraseña de la clave privada proporcionada con el certificado.

* El alias de la clave privada. Puede ejecutar el comando keytool de Java para ver el alias de la clave privada:
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* La contraseña del archivo del almacén de claves. Si utiliza el certificado de Extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de la clave privada.

Siga los siguientes pasos para configurar los certificados:

1. Inicie sesión en la instancia de autor de AEM como administrador. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
1. Haga clic en el campo **[!UICONTROL Nombre]** de la cuenta de usuario. Se abrirá la página **[!UICONTROL Editar configuración de usuario]**. En la instancia de autor de AEM, los certificados residen en un almacén de claves. Si no ha creado ningún almacén de claves anteriormente, haga clic en **[!UICONTROL Crear almacén de claves]** y establezca una nueva contraseña para el almacén. Si el servidor ya contiene un almacén de claves, omita este paso.  Si utiliza el certificado de Extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de la clave privada.
1. En la página **[!UICONTROL Editar configuración de usuario]**, seleccione la pestaña **[!UICONTROL Almacén de claves]**. Expanda la opción **[!UICONTROL Añadir clave privada del archivo del almacén de claves]** y proporcione un alias. El alias se utiliza para realizar la operación de las Extensiones de Reader.
1. Para cargar el archivo del certificado, haga clic en **[!UICONTROL Seleccionar archivo de almacén de claves]** y cargue un archivo &lt;filename>.pfx.

   Agregue la **[!UICONTROL Contraseña del almacén de claves]**, la **[!UICONTROL Contraseña de la clave privada]** y el **[!UICONTROL Alias de la clave privada]** asociados con el certificado a los campos respectivos. Haga clic en **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >En el entorno de producción, sustituya las credenciales de evaluación por credenciales de producción. Asegúrese de eliminar las credenciales antiguas de las Extensiones de Reader antes de actualizar una credencial caducada o de evaluaciones.

1. Haga clic en **[!UICONTROL Guardar y cerrar]** en la página **[!UICONTROL Editar configuración de usuario]**.

### Habilitar AES-256 {#enable-aes}

Para utilizar el cifrado AES 256 en archivos PDF, obtenga e instale los archivos de política de jurisdicción de fuerza ilimitada de la Extensión de criptografía de Java (JCE). Reemplace los archivos local_policy.jar y US_export_policy.jar en la carpeta jre/lib/security. Por ejemplo, si está utilizando el JDK de Sun, copie los archivos descargados en la carpeta `[JAVA_HOME]/jre/lib/security`.

El servicio Assembler depende del servicio Extensiones de Reader, del servicio Signature, del servicio Forms y del servicio Output. Realice los siguientes pasos para verificar que los servicios necesarios estén en funcionamiento:

1. Inicie sesión en la URL `https://'[server]:[port]'/system/console/bundles` como administrador.
1. Busque el siguiente servicio y asegúrese de que los servicios estén en funcionamiento:

<table>
 <tbody>
  <tr>
   <th>Nombre del servicio</th>
   <th>Nombre de paquete</th>
  </tr>
  <tr>
   <td>Servicio de firmas</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Servicio Extensiones de Reader</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Servicio de Forms</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>Servicio de salida</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

### (Solo Windows) Configure la entrada del Registro para Microsoft® Project {#configure-registry-entry-for-microsoft-project}

Después de instalar el complemento de AEM Forms y el proyecto Microsoft® en el equipo, registre una entrada para Microsoft® Project en la ubicación de 64 bits. Facilita la ejecución de pruebas de conversión de Project a PDFG. A continuación se indican los pasos que describen el proceso de entrada del Registro:

1. Abra el Editor del Registro de Microsoft® Windows (regedit), Para abrir el Editor del Registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
1. Vaya a `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`, cree un nuevo registro de **valor binario** y cambie su nombre a **Proyecto**.
1. Modifique el valor de datos del Registro binario creado a 01 y haga clic en Aceptar.
1. Cierre la entrada del Registro.


## Problemas y limitaciones conocidos {#known-issues-and-troubleshooting}

* La conversión de HTML a PDF falla si un archivo de entrada comprimido contiene archivos HTML con caracteres de doble byte en los nombres de archivo. Para evitar este problema, no utilice caracteres de doble byte al nombrar los archivos HTML.

* En sistemas operativos basados en UNIX, siga los siguientes pasos para encontrar las bibliotecas que faltan:

1. Navegue hasta `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Ejecute el siguiente comando para ver una lista de todas las bibliotecas que WebToPDF requiere para la conversión de HTML a PDF.

   `ldd phantomjs`

   Ejecute el siguiente comando para ver una lista de las bibliotecas que faltan.

   `ldd phantomjs | grep not`

1. Instale manualmente las bibliotecas que faltan.

## Herramienta de preparación del sistema (SRT) {#SRT}

La [Herramienta de preparación del sistema](#srt-configuration) comprueba si el equipo está configurado correctamente para ejecutar las conversiones de PDF Generator. La herramienta genera el informe en la ruta especificada. Para ejecutar la herramienta:

1. Abra el símbolo del sistema. Navegue hasta la carpeta `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools`.

1. Ejecute el siguiente comando desde el Símbolo del sistema:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   El comando genera el informe y también crea el archivo srt_config.yaml. Puede utilizarlo para configurar las opciones de la herramienta SRT. Es opcional configurar las opciones de la herramienta SRT.

   >[!NOTE]
   >
   >* Si la Herramienta de preparación del sistema informa de que el archivo pdfgen.api no está disponible en la carpeta de complementos de Acrobat, copie el archivo pdfgen.api del directorio `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` al directorio `[Acrobat_root]\Acrobat\plug_ins`.

1. Navegue hasta `[Path_of_reports_folder]`. Abra el archivo SystemReadinessTool.html. Compruebe el informe y corrija los problemas mencionados.

### Configuración de las opciones de la herramienta SRT {#srt-configuration}

Puede utilizar el archivo srt_config.yaml para configurar varias opciones de la herramienta SRT. El formato del archivo es el siguiente:

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
   #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
   locale: en
   
   #aemTempDir: AEM Temp direcotry
   aemTempDir:
   
   #users: provide PDFG converting users list
   #users:
   # - user1
   # - user2
   users:
   
   #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
   profile:
   
   #outputDir: directory where output files will be saved
   outputDir:
```

* **Configuración regional:** Es un parámetro obligatorio. Admite inglés(en), alemán (de), francés (fr) y japonés(ja). El valor predeterminado es en. No afecta a los servicios de PDF Generator que se ejecutan en AEM Forms en OSGi.
* **aemTempDir:** Es un parámetro opcional. Especifica la ubicación de almacenamiento temporal de Adobe Experience Manager.
* **usuarios:** Es un parámetro opcional. Puede especificar un usuario para comprobar si tiene los permisos necesarios y acceso de lectura y escritura en los directorios necesarios para ejecutar PDF Generator. Si no se especifica ningún usuario, las comprobaciones específicas del usuario se omiten y se muestran como erróneas en el informe.
* **outputDir:** Especifique la ubicación para guardar el informe SRT. La ubicación predeterminada es el directorio de trabajo actual de la herramienta SRT.

## Solución de problemas

Si tiene problemas incluso después de corregir todos los problemas notificados por la herramienta SRT, realice las siguientes comprobaciones:

Antes de realizar las siguientes comprobaciones, asegúrese de que [Herramienta de preparación del sistema](#SRT) no informa de ningún error.

+++ Adobe Acrobat

* Asegúrese de que solo están instaladas las [versiones compatibles](/help/sites-deploying/technical-requirements.md) de Microsoft® Office (32 bits) y Adobe Acrobat y de que se cancelan los cuadros de diálogo de apertura.
* Asegúrese de que el servicio Update de Adobe Acrobat esté deshabilitado.
* Asegúrese de que el archivo por lotes [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) se ha ejecutado con privilegios de administrador.
* Asegúrese de que se agrega un usuario de PDF Generator en la interfaz de usuario de la configuración de PDF.
* Asegúrese de que se agrega el permiso [Reemplazar un (símbolo) token de nivel de proceso](#grant-the-replace-a-process-level-token-privilege) al usuario de PDF Generator.
* Asegúrese de que el complemento Acrobat PDFMaker Office COM esté habilitado para las aplicaciones de Microsoft Office.

+++

+++OpenOffice

**Microsoft® Windows**

* Asegúrese de que la [versión compatible](/help/sites-deploying/technical-requirements.md) de 32 bits de Microsoft Office está instalada y de que los cuadros de diálogo de apertura se cancelan para todas las aplicaciones.
* Asegúrese de que se agrega un usuario de PDF Generator en la interfaz de usuario de la configuración de PDF.
* Asegúrese de que el usuario de PDF Generator sea miembro del grupo de administradores y de que se establece el privilegio [Reemplazar un (símbolo) token de nivel de proceso](#grant-the-replace-a-process-level-token-privilege) para el usuario.
* Asegúrese de que el usuario está configurado en la interfaz de usuario de PDF Generator y realiza las siguientes acciones:
   1. Inicie sesión en Microsoft® Windows con el usuario de PDF Generator.
   1. Abra las aplicaciones de Microsoft® Office u OpenOffice y cancele todos los cuadros de diálogo.
   1. Establezca AdobePDF como la impresora predeterminada.
   1. Establezca Acrobat como el programa predeterminado para los archivos PDF.
   1. Realice la conversión manual mediante las opciones Archivo > Imprimir y Acrobat de la cinta de opciones de las aplicaciones de Microsoft Office y cancele todos los cuadros de diálogo.
   1. Finalice todos los procesos relacionados con la conversión, como winword.exe, powerpoint.exe y excel.exe.
   1. Reinicie el servidor de AEM Forms.

**Linux®**

* Instale la versión compatible de OpenOffice. AEM Forms admite versiones de 32 y 64 bits. Después de la instalación, abra todas las aplicaciones de OpenOffice, cancele todas las ventanas de diálogo y cierre las aplicaciones. Vuelva a abrir las aplicaciones y asegúrese de que no aparece ningún cuadro de diálogo al abrir una aplicación de OpenOffice.

* Cree una variable de entorno `OpenOffice_PATH` y configúrela para que apunte a que la instalación de OpenOffice está establecida en la [consola](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) o en el perfil dt (árbol de dispositivos).
* Si hay problemas al instalar OpenOffice, asegúrese de que las [bibliotecas de 32 bits](#extrarequirements) requeridas para la instalación de OpenOffice están disponibles.

+++

Problemas de conversión de ++HTML a PDF

* Asegúrese de que los directorios de fuentes se agregan en la interfaz de usuario de la configuración de PDF Generator.

**Linux y Solaris (ruta de conversión WebToPDF)**

* Asegúrese de que la biblioteca de 32 bits esté disponible (libicudata.so.42) para la conversión HTMLoPDF basada en Webkit y que las bibliotecas de 64 bits (libicudata.so.42) estén disponibles para la conversión HTMLoPDF basada en WebToPDF.

* Ejecute el siguiente comando para ver una lista de las bibliotecas que faltan para WebToPDF:

  ```
  ldd phantomjs | grep not
  ```

**Linux® y Solaris™ (ruta de conversión WebKit)**

* Asegúrese de que los directorios `/usr/lib/X11/fonts` y `/usr/share/fonts` existen. Si los directorios no existen, cree un vínculo simbólico desde `/usr/share/X11/fonts` a `/usr/lib/X11/fonts` y otro vínculo simbólico de `/usr/share/fonts` a `/usr/share/X11/fonts`.

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* Asegúrese de que las fuentes de IBM se copien en usr/share/fonts.
* Asegúrese de que la corrección de vulnerabilidades fantasma glibc esté disponible en el equipo. Utilice su gestor de paquetes predeterminado para actualizar a la última versión de glibc. Incluye corrección de vulnerabilidades fantasma.
* Asegúrese de que las últimas versiones de las bibliotecas lib curl, libcrypto y libssl de 32 bits estén instaladas en el sistema. Cree también enlaces simbólicos `/usr/lib/libcurl.so` (o libcurl.a para AIX®), `/usr/lib/libcrypto.so` (o libcrypto.a para AIX®) y `/usr/lib/libssl.so` (o libssl.a para AIX®) que apunten a las últimas versiones (32 bits) de las bibliotecas correspondientes.

* Realice los siguientes pasos para el proveedor de sockets SSL de IBM®:
   1. Copie el archivo java.security de `<WAS_Installed_JAVA>\jre\lib\security` a una ubicación del servidor de AEM Forms. La ubicación predeterminada es Ubicación predeterminada es = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Edite el archivo java.security en la ubicación copiada y cambie las fábricas de sockets SSL predeterminadas por fábricas JSSE2 (utilice fábricas JSSE2 en lugar de WebSphere®).

      Cambie las siguientes fábricas de sockets JSSE predeterminadas:

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      a

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ No se puede agregar un usuario de PDF Generator (PDFG)

* Asegúrese de que Microsoft® Visual C++ 2012 x86 y Microsoft® Visual C++ 2013 x86 (32 bits) redistribuibles estén instalados en Windows.

+++

+++Errores en la prueba de automatización

* Realice al menos una conversión manual en Microsoft® Office y OpenOffice (con cada usuario) para asegurarse de que no aparece ningún cuadro de diálogo durante la conversión. Si aparece algún diálogo, descártelo. No debería aparecer ningún cuadro de diálogo de este tipo durante la conversión automatizada.

* Antes de ejecutar la automatización en un entorno OSGi de AEM Forms, asegúrese de que el paquete de prueba esté instalado y activo.

+++

+++Errores en la conversión de varios usuarios

* Compruebe los registros del servidor para comprobar si se están produciendo errores en las conversiones realizadas por un usuario en particular.(El Explorador de procesos puede ayudarle a comprobar el proceso de ejecución de distintos usuarios)

* Asegúrese de que el usuario configurado para el PDF Generator tiene derechos de administrador local.

* Asegúrese de que el usuario de PDF Generator tenga permisos de lectura, escritura y ejecución en los usuarios temporales LC y PDFG.

* Realice al menos una conversión manual en Microsoft® Office y OpenOffice (con cada usuario) para asegurarse de que no aparece ningún cuadro de diálogo durante la conversión. Si aparece algún diálogo, descártelo. No debería aparecer ningún cuadro de diálogo de este tipo durante la conversión automatizada.

* Realice una conversión de prueba.

+++

+++La licencia de Adobe Acrobat instalada en el servidor de AEM Forms caduca

* Si tiene una licencia existente de Adobe Acrobat y esta ha caducado, [descargue la versión más reciente de Adobe Application Manager](https://helpx.adobe.com/es/creative-suite/kb/aam-troubleshoot-download-install.html) y migre el número de serie. Antes de [migrar el número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Utilice los siguientes comandos para generar el archivo prov.xml y vuelva a serializar la instalación existente usando este en lugar de los comandos proporcionados en el artículo [Migración del número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

         ```
         
         adobe_prtk --tool=VolumeSerialize --generate --serial=&lt;serialnum> [--leid=&lt;LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=lista de configuraciones regionales en formato xx_XX format o ALL>] [--provfile=&lt;Ruta absoluta de prov.xml>]
         
         ```
     
   * Serialice el paquete por volumen (vuelva a serializar la instalación existente usando el archivo prov.xml y la nueva serie): ejecute el siguiente comando desde la carpeta de instalación PRTK como administrador para serializar y activar los paquetes implementados en los equipos cliente:

         ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
         ```
     
* Para instalaciones a gran escala, utilice [Customization Wizard de Acrobat](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) para eliminar las versiones anteriores de Reader y Acrobat. Personalice el programa de instalación e impleméntelo en todos los equipos de su organización.

+++

+++ El servidor de AEM Forms se encuentra en un entorno seguro o sin conexión, e Internet no está disponible para activar Acrobat.

* Puede conectarse en un plazo de 7 días a partir del primer inicio del producto de Adobe para realizar la activación y el registro en línea o utilizar un dispositivo con acceso a Internet y el número de serie del producto para completar este proceso. Para obtener instrucciones detalladas, consulte [Activación sin conexión](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=es).

+++

+++ No se pueden convertir archivos de Word o Excel a PDF en Windows Server

Cuando el usuario intenta convertir archivos de Word o Excel a PDF en Microsoft Windows Server, se encuentra el siguiente error:

*Mensaje de error del convertidor principal: ALC-PDG-015-003-El sistema no puede abrir el archivo de entrada. Vuelva a enviar el archivo o póngase en contacto con el administrador del sistema.*

Para resolver el problema, consulte [No se puede convertir el archivo de Word o Excel al PDF en Windows Server](/help/forms/using/disable-uac-for-pdfgconfiguration.md).

+++

+++ No se pueden convertir archivos de Excel a PDF en Windows Server 2019

Al convertir Microsoft Excel 2019 a PDF en Microsoft Windows Server 2019, debe asegurarse de lo siguiente:

* Al utilizar el servicio PDF Generator, el equipo Windows no debe tener ninguna conexión remota activa con el servidor de AEM (sesión RDP de Windows).
* La impresora predeterminada debe establecerse en Adobe PDF.

  >[!NOTE]
  >* Para Apple macOS y el sistema operativo Ubuntu, no es necesario configurar las opciones mencionadas.

+++

+++ No se pueden convertir archivos XPS a PDF

Para resolver el problema, [cree una clave de registro específica de la característica en Windows](https://helpx.adobe.com/in/acrobat/kb/unable-convert-xps-to-pdfs.html).

+++


## Pasos siguientes {#next-steps}

Tiene un entorno de AEM Forms Document Services en funcionamiento. Puede utilizar Document Services mediante lo siguiente:

* [Flujos de trabajo centrados en Forms en OSGi](/help/forms/using/aem-forms-workflow.md)
* [Carpetas inspeccionadas](/help/forms/using/watched-folder-in-aem-forms.md)
* [API de Document Services](/help/forms/using/aem-document-services-programmatically.md)
