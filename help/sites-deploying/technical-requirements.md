---
title: Requisitos técnicos
description: Una lista de las plataformas de cliente y servidor compatibles con Adobe Experience Manager.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: f65dd129-9e28-4de1-acca-dd31eaf3c19b
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '2960'
ht-degree: 13%

---

# Requisitos técnicos{#technical-requirements}

Adobe admite (AEM) Adobe Experience Manager en las plataformas, tal como se detalla en la siguiente información de este documento.

Para cualquier problema relacionado con la plataforma, póngase en contacto con el proveedor de la plataforma.

>[!NOTE]
>
>Según la plataforma en la que instale AEM, podría haber diferentes conjuntos de requisitos para la administración de usuarios.

## Requisitos previos {#prerequisites}

Requisitos mínimos para instalar Adobe Experience Manager:

* Java™ Platform, Standard Edition JDK u otras [máquinas virtuales Java™ compatibles](#java-virtual-machines) instaladas
* Archivo de inicio rápido de Experience Manager (JAR independiente o WAR de implementación de aplicación web)

### Requisitos mínimos de tamaño {#minimum-sizing-requirements}

Requisitos mínimos para ejecutar Adobe Experience Manager:

* 5 GB de espacio libre en disco en el directorio de instalación
* 2 GB de memoria

>[!NOTE]
>
>* Los casos de uso de recursos digitales necesitan más memoria base. Consulte [Implementación y mantenimiento](/help/sites-deploying/deploy.md#default-local-install) para obtener más información.
>* [El paquete de complementos de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) requiere 15 GB de espacio temporal.
>

Para obtener más información, consulte las [Directrices de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md).

### Niveles de compatibilidad {#support-levels}

Este documento enumera las plataformas de cliente y servidor compatibles con Adobe Experience Manager. Adobe proporciona varios niveles de compatibilidad, tanto para las configuraciones recomendadas como para otras configuraciones.

### Configuraciones compatibles {#supported-configurations}

Adobe recomienda estas configuraciones y proporciona soporte total como parte del acuerdo de mantenimiento de software estándar.

<table>
 <tbody>
  <tr>
   <td>Nivel de soporte</td>
   <td>Descripción<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Compatible</strong></td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad de Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Compatibilidad restringida</strong></td>
   <td>Para garantizar el éxito del proyecto de los clientes, Adobe proporciona soporte completo dentro de un programa de soporte restringido, que requiere que se cumplan condiciones específicas. El soporte de nivel R requiere una solicitud de cliente formal y la confirmación de Adobe. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe.</td>
  </tr>
 </tbody>
</table>

### Configuraciones no admitidas {#unsupported-configurations}

| Nivel de soporte | Descripción |
|---|---|
| **Z: no compatible** | La configuración no es compatible. Adobe no realiza ninguna declaración sobre si la configuración funciona o no, y no la admite. |

## Plataformas compatibles {#supported-platforms}

### Java™ máquinas virtuales {#java-virtual-machines}

La aplicación requiere una máquina virtual Java™ para ejecutarse, que proporciona la distribución Java™ Development Kit (JDK).

Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java™:

>[!CAUTION]
>
>Realice un seguimiento de los boletines de seguridad del proveedor de Java™. Al hacerlo, se garantiza la seguridad de los entornos de producción. Además, instale siempre las últimas actualizaciones de Java™.

| **Plataforma** | **Nivel de soporte** | **Vincular** |
|---|---|---|
| Oracle Java™ SE 17 JDK | A: Compatible `[1]` |
| Oracle Java™ SE 21 JDK | A: Compatible `[1]` |
| VM de IBM® Semeru J9 - compilación 17.0.13.0 | A: Compatible `[2]` |
| VM de IBM® Semeru J9 - compilación 21.0.6.0 | A: Compatible `[2]` |

1. Oracle se ha trasladado a un modelo de &quot;Soporte a largo plazo&quot; (LTS) para los productos de Oracle Java™ SE. Java™ 9, Java™ 10, Java™ 12, Java™ 13, Java™ 14, Java™ 15m Java™ 16 son versiones que no son de LTS de Oracle (consulte [Guía de asistencia de Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implementar AEM en un entorno de producción, Adobe solo es compatible con las versiones LTS de Java™. El soporte y la distribución del JDK de Oracle Java™ SE, incluidas todas las actualizaciones de mantenimiento de las versiones de LTS más allá del final de las actualizaciones públicas, son compatibles directamente con Adobe para todos los clientes de AEM que utilizan la tecnología Oracle Java™ SE. Consulte la [directiva de soporte de Java™ para Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Esta versión es compatible con Oracle Java™ 17 y Oracle Java™ 21.**

1. El JRE de IBM® solo se admite junto con el servidor de aplicaciones WebSphere®.

### Almacenamiento y persistencia {#storage-persistence}

Existen varias opciones para implementar el repositorio de Adobe Experience Manager. Consulte la siguiente lista para ver las tecnologías compatibles y las opciones de almacenamiento.

| **Plataforma** | **Descripción** | **Nivel de soporte** |
|---|---|---|
| **Sistema de archivos con archivos TAR** `[1]` | Repositorio | A: Compatible |
| **Sistema de archivos con almacén de datos** `[1]` | Binarios | A: Compatible |
| Almacenar binarios en archivos TAR en el sistema de archivos `[1]` | Binarios | Z: No compatible con la producción |
| Amazon S3 | Binarios | A: Compatible |
| Microsoft® Azure Blob Storage | Binarios | A: Compatible |
| MongoDB Enterprise 6.0 y 7.0 | Repositorio | A: Compatible `[3, 4]` |
| **Apache Lucene (integrado en Quickstart)** | Servicio de búsqueda | A: Compatible |

1. &quot;File System&quot; incluye almacenamiento en bloque compatible con POSIX. Incluye tecnología de almacenamiento en red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Cargar AEM de prueba con el sistema de archivos de red/remoto.
1. El uso compartido de MongoDB no es compatible con AEM.
1. El motor de almacenamiento MongoDB WiredTiger solo es compatible.

>[!NOTE]
>
>MongoDB es un programa de software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Directiva de licencias de MongoDB](https://www.mongodb.com/licensing/server-side-public-license/faq).
>
>Para aprovechar al máximo su implementación de AEM con MongoDB, Adobe recomienda licenciar la versión de MongoDB Enterprise para beneficiarse del soporte profesional. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obtener más información.
>
>La licencia incluye un conjunto de réplicas estándar, que está compuesto por una instancia principal y dos secundarias que se pueden utilizar para las implementaciones de autor o publicación.
>
>Si desea ejecutar tanto la creación como la publicación en MongoDB, se deben adquirir dos licencias independientes.
>
>El Servicio de atención al cliente de Adobe ayuda a calificar los problemas relacionados con el uso de MongoDB con AEM.
>
>Para obtener más información, consulte la [Página MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

### Motores servlet/servidores de aplicaciones {#servlet-engines-application-servers}

Adobe Experience Manager se puede ejecutar como servidor independiente (el archivo JAR de inicio rápido) o como aplicación web dentro de un servidor de aplicaciones de terceros (el archivo WAR).

La versión mínima de la API de servlet requerida es Servlet 3.1. Además, AEM admite el servlet 5 de Jakarta para jar y war se puede implementar en servidores de aplicaciones que implementen la API 5/6 del servlet de Jakarta.

| Plataforma | Nivel de soporte |
|---|---|
| **Motor de servlet integrado Quickstart (Jetty 11.0.x)** | A: Compatible |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) con Perfil web 24.0.0.7 y IBM® Sumeru open JRE® 17/21 | R: Compatibilidad restringida para nuevos contratos `[1]` |
| Apache Tomcat 10.0.x/10.1.x | R: Compatibilidad restringida para nuevos contratos `[1]` |

1. Al iniciar implementaciones de AEM 6.5 en servidores de aplicaciones, se pasa a Compatibilidad restringida. Los clientes existentes pueden actualizar a AEM 6.5 y seguir utilizando servidores de aplicaciones. Para nuevos clientes, incluye criterios de asistencia y un programa de asistencia, tal como se indica en la descripción del nivel R anterior.

### Sistemas operativos del servidor {#server-operating-systems}

Adobe Experience Manager funciona con las siguientes plataformas de servidor para entornos de producción:

| **Plataforma** | **Nivel de soporte** |
|---|---|
| **Linux®, basado en la distribución Red Hat®** | A: Compatible `[1]` `[2]` |
| Linux®, basado en la distribución Debian incl. Ubuntu | A: Compatible `[1]` |
| Linux®, basado en la distribución SUSE® | A: Compatible `[1]` |
| Microsoft® Windows Server 2022 | R: Compatible |

1. Linux® Kernel 5. x y 6. x incluye derivados de la distribución Red Hat®, incluidos Red Hat® Enterprise Linux®, CentOS, Oracle Linux® y Amazon Linux®.
1. Distribución Linux® compatible con Adobe Managed Services.

   >[!NOTE]
   >
   >Para servidores basados en Linux, los complementos de AEM Forms requieren dependencias de tiempo de ejecución como:
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64 (1.13-1.el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64 (2.17 o posterior)


### Entornos de computación virtual y en la nube {#virtual-cloud-computing-environments}

Adobe Experience Manager es compatible con la ejecución en una máquina virtual en entornos de computación en la nube. Estos entornos incluyen, como Microsoft® Azure y Amazon Web Service (AWS), que se ejecutan de conformidad con los requisitos técnicos enumerados en esta página y según los términos de soporte estándar de Adobe.

Para un entorno nativo de la nube, revise la última oferta de la línea de productos de AEM: Adobe Experience Manager as a Cloud Service. Consulte [Documentación de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) para obtener más información.

Adobe también ofrece Adobe Managed Services para implementar AEM en Azure o AWS. Adobe Managed Services ofrece a los expertos la experiencia y los conocimientos necesarios para implementar y utilizar AEM en estos entornos de cloud computing. Ver [documentación adicional sobre Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

En todos los demás casos de implementación de AEM en Azure o AWS, o en cualquier otro entorno de computación en la nube, la compatibilidad con Adobe se incluye en el entorno de computación virtual. Ese entorno virtual debe ejecutarse de acuerdo con las especificaciones técnicas enumeradas en esta página. Cualquier problema informado relativo a AEM que se ejecute en cualquiera de estos entornos de nube debe ser reproducible independientemente de cualquier servicio de nube específico para el entorno de computación en nube. Es decir, a menos que el servicio en la nube sea compatible como parte de los requisitos técnicos enumerados en esta página, por ejemplo, Azure Blob Storage o AWS S3.

Para obtener recomendaciones sobre cómo implementar AEM en Azure o AWS, fuera de Adobe Managed Services, Adobe recomienda trabajar directamente con el proveedor de la nube. O bien, trabajar con socios de Adobe que apoyen la implementación de AEM en el entorno de nube que elija. El proveedor o socio de nube seleccionado es responsable de las especificaciones de tamaño, el diseño y la implementación de la arquitectura, para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.

### Plataformas Dispatcher (servidores web) {#dispatcher-platforms-web-servers}

Dispatcher es el componente de almacenamiento en caché y equilibrio de carga. [Descargar la versión más reciente de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html). Experience Manager 6.5 requiere Dispatcher versión 4.3.2 o superior.

Los siguientes servidores web son compatibles con la versión 4.3.2 de Dispatcher:

| Plataforma | Nivel de soporte |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Compatible |
| Microsoft® IIS 10 (Internet Information Server) | A: Compatible |
| Microsoft® IIS 8.5 (Internet Information Server) | Z: No compatible |

1. Los servidores web creados en función del código fuente Apache httpd son tan compatibles como la versión de httpd en la que se basan. En caso de duda, solicite a Adobe la confirmación del nivel de asistencia relacionado con el producto del servidor correspondiente. Los casos siguientes:

   1. El servidor HTTP se creó utilizando solo distribuciones de origen oficiales de Apache, o
   1. El servidor HTTP se entregó como parte del sistema operativo en el que se está ejecutando. Ejemplos: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher no está disponible para los sistemas operativos Apache 2.4.x para Windows.

## Plataformas de cliente compatibles {#supported-client-platforms}

### Exploradores admitidos para la interfaz de usuario de creación {#supported-browsers-for-authoring-user-interface}

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente. Todos los exploradores se prueban con el conjunto predeterminado de complementos.

La interfaz de usuario de AEM está optimizada para pantallas más grandes (normalmente portátiles y equipos de escritorio) y formatos de tableta (como Apple iPad o Microsoft® Surface). El factor de forma del teléfono no es compatible.

>[!NOTE]
>
>**Compatibilidad con exploradores con ciclos de lanzamiento rápidos:**
>
>Mozilla Firefox, Google Chrome y Microsoft® Edge se actualizan cada pocos meses. Adobe se compromete a proporcionar actualizaciones para Adobe Experience Manager a fin de mantener el nivel de compatibilidad que se indica a continuación con las próximas versiones de estos exploradores.

<table>
 <tbody>
  <tr>
   <td><strong>Explorador</strong></td>
   <td><strong>Compatibilidad con la IU de<br /> </strong></td>
   <td><strong>Compatibilidad con la IU clásica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Mozilla Firefox última ESR [1]</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en macOS (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x en macOS</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 12.x</td>
   <td>A: Compatible [2]</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 11.x</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
 </tbody>
</table>

1. Lanzamiento de soporte ampliado de Firefox [Más información en mozilla.org](https://www.mozilla.org/es-ES/firefox/enterprise/)
1. Compatibilidad con Apple iPad

### Exploradores compatibles con los sitios web {#supported-browsers-for-websites}

Por lo general, la compatibilidad del explorador con los sitios web procesados por AEM Sites depende de la implementación de las plantillas de página de AEM, el diseño y la salida de componentes y, por lo tanto, depende del control de la parte que implementa estas partes.

## Notas de plataforma adicionales {#additional-platform-notes}

Esta sección proporciona notas especiales e información más detallada sobre la ejecución de Adobe Experience Manager y sus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de Adobe Experience Manager (Instance, Dispatcher) se pueden instalar en redes IPv4 e IPv6.

El funcionamiento es fluido, ya que no se requiere ninguna configuración especial. Si es necesario, especifique una dirección IP con el formato adecuado para el tipo de red.

Cuando se debe especificar una dirección IP, se puede seleccionar (según sea necesario) una de las siguientes opciones:

* Una dirección IPv6. Por ejemplo, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Una dirección IPv4. Por ejemplo, `https://123.1.1.4:4502`

* Un nombre de servidor. Por ejemplo, `https://www.yourserver.com:4502`

* El caso predeterminado de `localhost` se interpreta para las instalaciones de red IPv4 e IPv6. Por ejemplo, `https://localhost:4502`

### Requisitos del complemento Dynamic Media de AEM {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está desactivado de forma predeterminada. Vea aquí [para habilitar Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Media habilitado, se aplican los siguientes requisitos técnicos adicionales.

>[!NOTE]
>
>Estos requisitos del sistema **solo se aplican** si usa Dynamic Media (modo híbrido); Dynamic Media (modo híbrido) tiene un servidor de imágenes incrustado, que solo está certificado en determinados sistemas operativos.
>
>Para los clientes de Dynamic Media que ejecutan el modo Dynamic Media - Scene7 (es decir, el modo de ejecución de **dynamicmedia_scene7**), no hay requisitos de sistema adicionales; solo los mismos requisitos de sistema que AEM. Dynamic Media: la arquitectura de modo de Scene7 utiliza el servicio de imágenes basado en la nube y no el servicio incrustado en AEM.

#### Hardware {#hardware}

Los siguientes requisitos de hardware son aplicables tanto para Linux® como para Windows:

* Intel Xeon® o AMD® Opteron CPU con al menos cuatro núcleos
* Al menos 16 GB de RAM

#### Linux® {#linux}

Si utiliza Dynamic Media en Linux®, se deben cumplir los siguientes requisitos previos:

* Red Hat® Enterprise 7 o CentOS 7 y versiones posteriores con los parches de correcciones más recientes
* Sistema operativo de 64 bits
* Intercambio desactivado (recomendado)
* SELinux desactivado (Consulte la nota que sigue)

>[!NOTE]
>
>Si la configuración regional está configurada de tal manera que LC_CTYPE no es igual a `en_US.UTF-8`, impide que Dynamic Media funcione. Para ver su valor, escriba &quot;locale&quot; en el símbolo del sistema. Si no se configura correctamente, establezca la variable de entorno LC_CTYPE en la cadena vacía escribiendo &quot;export LC_CTYPE=&quot; antes de ejecutar AEM.

>[!NOTE]
>
>**Al deshabilitar SELinux:** el servicio de imágenes no funciona con SELinux activado. Esta opción está habilitada de forma predeterminada. Para solucionar este problema, edite el archivo **/etc/selinux/config** y cambie el valor SELinux de:
>
>`SELINUX=enforcing` **a** `SELINUX=disabled`

>[!NOTE]
>
>**Arquitectura NUMA:** Los sistemas con procesadores AMD64 e Intel® EM64T suelen configurarse como plataformas de arquitectura de memoria no uniforme (NUMA). Es decir, el núcleo construye varios nodos de memoria durante el arranque en lugar de construir un solo nodo de memoria.
>
>La construcción de varios nodos puede causar agotamiento de la memoria en uno o más de los nodos antes de que otros nodos se agoten. Cuando se agota la memoria, el núcleo puede decidir matar procesos (por ejemplo, el servidor de imágenes o el servidor de plataforma) aunque haya memoria disponible.
>
>Por lo tanto, Adobe recomienda que si está ejecutando un sistema de este tipo, desactive NUMA usando la opción de arranque **numa=off** para evitar que el núcleo destruya estos procesos.

>[!NOTE]
>
>**El nombre de host del servidor debe resolverse:** Asegúrese de que el nombre de host del servidor puede resolverse en una dirección IP. Si no es posible, agregue el nombre de host completo y la dirección IP a **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Intercambiar el espacio al menos el doble de la cantidad de memoria física (RAM)

Para utilizar Dynamic Media en Windows, instale Microsoft® Visual Studio 2010, 2013 y 2015 redistribuible para x64 y x86.

Para Windows x64:

* Obtenga Microsoft® Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Obtenga Microsoft® Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenga Microsoft® Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenga Microsoft® Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Obtenga Microsoft® Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenga Microsoft® Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x y posterior
* Solo se admite con fines de prueba y demostración

### Requisitos para AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

### Soporte de software para el generador de PDF {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto</strong></p> </th>
   <th><p><strong>Formatos compatibles para la conversión a PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 classic track</a> última versión</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF y DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF y TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El generador de PDF solo admite versiones en alemán, francés, inglés y japonés de los sistemas operativos y aplicaciones compatibles.
>
>Además,
>
>* PDF Generator requiere una versión de 32 bits de [Acrobat 2020 classic track versión 20.004.30006](https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versión 17.011.30078 para realizar la conversión.
>* PDF Generator solo admite la versión comercial de 32 bits de Microsoft® Office Professional Plus y otro software necesario para la conversión.
>* La instalación de Microsoft® Office Professional Plus puede utilizar licencias por volumen basadas en Retail o MAK/KMS/AD.
>* Si una instalación de Microsoft® Office se desactiva o deja de tener licencia debido a algún motivo, como una instalación con licencia por volumen que no puede localizar un host KMS en un período especificado, las conversiones pueden fallar hasta que se vuelva a otorgar la licencia a la instalación y se vuelva a activar.
>* PDF Generator admite las versiones de 32 y 64 bits de OpenOffice en el sistema operativo Linux®.
>* PDF Generator no admite Microsoft® Office 365.
>* Las conversiones de PDF Generator para OpenOffice solo son compatibles con Windows y Linux®.
>* Las características de PDF, Optimizar PDF y Exportar PDF de OCR solo son compatibles con Windows.
>* Una versión de Acrobat se incluye con AEM Forms para habilitar la funcionalidad Generador de PDF. Mediante programación, acceda a la versión agrupada solo con AEM Forms, durante el período de licencia de AEM Forms, para utilizarlo con AEM Forms PDF Generator. Para obtener más información, consulte la descripción del producto de AEM Forms según su implementación ([Local](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* El servicio PDF Generator no es compatible con Microsoft® Windows 10.
>* PDF Generator no puede convertir archivos con Microsoft® Visio 2019. Puede seguir utilizando Microsoft® Visio 2016 para convertir `.VSD` y `.VSDX` archivos.
>* PDF Generator no puede convertir archivos con Microsoft® Project 2019. Puede seguir utilizando Microsoft® Project 2016 para convertir `.VSD` y `.VSDX` archivos.
>

### Requisitos para AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 o Windows® 11
* Procesador de 1 GHz o más rápido con soporte para PAE, NX y SSE2.
* 1 GB de RAM para 32 bits o 2 GB de RAM para SO de 64 bits;
* 16 GB de espacio en disco para 32 bits o 20 GB de espacio en disco para SO de 64 bits;
* Memoria gráfica: 128 MB de GPU (se recomiendan 256 MB);
* 2,35 GB de espacio disponible en disco duro;
* 1024 X 768 píxeles de resolución de monitor o superior;
* Aceleración de hardware de vídeo (opcional);
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC
* Privilegios administrativos para instalar Designer
* Tiempo de ejecución de 32 bits de Microsoft Visual C++ 2019 (VC 14.28 o superior) para AEM Forms Designer de 32 bits
* Tiempo de ejecución de 64 bits de Microsoft Visual C++ 2019 (VC 14.28 o superior) para AEM Forms Designer de 64 bits

[Instalar y configurar AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)

### Requisitos para la reescritura de metadatos de XMP de AEM Assets {#requirements-for-aem-assets-xmp-metadata-write-back}

La reescritura de XMP es compatible y está habilitada para las siguientes plataformas y formatos de archivo:

* **Sistemas operativos:**

   * Linux® (compatibilidad con aplicaciones de 32 y 32 bits en sistemas de 64 bits).
   * Windows Server
   * macOS X (64 bits)

* **Formatos de archivo**: JPEG, PNG, TIFF, PDF, INDD, AI y EPS.

### Requisitos para que los AEM Assets procesen recursos con muchos metadatos en Linux® {#assetsonlinux}

El proceso XMPFilesProcessor requiere la biblioteca GLIBC_2.14 para funcionar. Utilice un núcleo Linux® que contenga GLIBC_2.14, por ejemplo, Linux® kernel versión 3.1.x. Mejora el rendimiento para procesar recursos que contienen una gran cantidad de metadatos, como archivos PSD. El uso de una versión anterior de GLIBC produce un error en los registros que comienzan por `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
