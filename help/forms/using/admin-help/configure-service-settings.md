---
title: Configurar los ajustes del servicio
description: Obtenga información sobre cómo configurar los ajustes del servicio. Puede utilizar la página Administración de servicios para configurar los ajustes de cada uno de los servicios que forman parte de los formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a2586a1e-0e7f-4ea4-87ec-fbd82df3ec4c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '10836'
ht-degree: 4%

---

# Configurar los ajustes del servicio {#configure-service-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede usar la página Administración de servicios para establecer la configuración de cada uno de los servicios que forman parte de los formularios de AEM. La configuración disponible varía en función del servicio que se esté configurando.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Detenga el servicio antes de cambiarlo. (Consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Haga clic en el nombre del servicio que desea configurar.
1. Si el servicio tiene una pestaña Configuración, utilícela para cambiar la configuración del servicio. Consulte la lista de vínculos a continuación para obtener más información.

   >[!NOTE]
   >
   >No todos los servicios enumerados en la página Administración de servicios tienen una ficha Configuración. En el caso de los procesos que ha creado, la pestaña Configuración solo aparece si ha añadido un parámetro de configuración al proceso en Workbench. (Consulte &quot;Parámetros de configuración&quot; en la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Haga clic en la ficha Seguridad y establezca la configuración de seguridad del servicio. Consulte [Modificación de la configuración de seguridad de un servicio](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Si el servicio tiene una pestaña Puntos finales, utilícela para cambiar la configuración del punto de conexión. Consulte [Administración de extremos](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Haga clic en la ficha Agrupamiento y defina la configuración de agrupación. Consulte [Configuración de agrupación para un servicio](configure-service-settings.md#configuring-pooling-for-a-service).
1. Haga clic en Guardar para guardar los cambios o haga clic en Cancelar para descartarlos.
1. Seleccione la casilla de verificación situada junto al nombre del servicio y haga clic en Start para reiniciarlo.

## Configuración del servicio Auditar flujo de trabajo {#audit-workflow-service-settings}

Workbench proporciona la capacidad de registrar instancias de proceso a medida que se ejecutan en tiempo de ejecución y luego reproducirlas para observar el comportamiento del proceso. (Consulte la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Para conservar espacio en el sistema de archivos de Forms Server, puede limitar la cantidad de datos de registro de procesos que se almacenan. Puede configurar las siguientes propiedades del servicio de flujo de trabajo de auditoría ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** El número máximo de grabaciones almacenadas. Cuando se almacena el número máximo, la grabación más antigua se elimina del sistema de archivos cuando se crea una nueva grabación. Esta propiedad es útil si tiende a crear muchas grabaciones y desea quitar automáticamente las antiguas. El valor predeterminado es 50.

**MaxNumberOfRecordingEntries:** Número máximo de entradas de datos que se pueden almacenar para cada grabación. Las entradas de datos son información sobre las operaciones del proceso. Se almacenan varias entradas para cada ejecución de una operación, como si se inició la operación, si se completó la operación y si se completó la ruta que lleva a la operación. Esta propiedad es útil cuando los procesos pueden incluir muchas ejecuciones de operaciones, por ejemplo, cuando se encuentra un bucle interminable. El valor predeterminado es 50.

## configuración del servicio de formularios con códigos de barras {#barcoded-forms-service-settings}

El servicio de formularios con códigos de barras `(BarcodedFormsService)` extrae datos de códigos de barras de imágenes digitalizadas. El servicio acepta un formulario con códigos de barras (TIFF o PDF) como entrada y extrae la representación automática de los datos codificados por el código de barras.

Las siguientes configuraciones están disponibles para el servicio de formularios con códigos de barras.

**Leer a la izquierda:** Cuando se seleccionan, las imágenes de código de barras se analizan horizontalmente de derecha a izquierda.

**Leer a la derecha:** Cuando se seleccionan, las imágenes de código de barras se analizan horizontalmente de izquierda a derecha.

**Leer:** Cuando se seleccionan, las imágenes de código de barras se analizan verticalmente de abajo a arriba.

**Leer más abajo:** Cuando se seleccionan, las imágenes de código de barras se analizan verticalmente de arriba abajo.

>[!NOTE]
>
>De forma predeterminada, se seleccionan todas las opciones. Anule la selección de una opción solo si está seguro de que no aparecerán códigos de barras de esa manera en los formularios.

**Ruta de acceso del archivo base:** Ruta de acceso del archivo relativa a la cual se resuelven los parámetros de archivo de entrada y salida del lote para las operaciones Ejecutar trabajo de archivo XML y Ejecutar trabajo de archivo plano. En las configuraciones agrupadas, la ruta de acceso base del archivo debe ser una ubicación compartida del sistema de archivos a la que todos los nodos del clúster tengan acceso de lectura y escritura.

**Nombre de Data Source:** Nombre del origen de datos que se usa para mantener la información de estado e historial de los trabajos de procesamiento por lotes. La fuente de datos especificada debe admitir transacciones globales (XA).

## Configuración del servicio Bridge de migración central (obsoleto) {#central-migration-bridge-service-settings}

El servicio Bridge de migración central (`CentralMigrationBridge`) invoca un subconjunto de la funcionalidad de Adobe Central Pro Output Server (Central), que incluye los comandos JFMERGE, JFTRANS y XMLIMPORT. Las operaciones del servicio de migración central de Bridge le permiten reutilizar los siguientes recursos centrales en los formularios de AEM:

* diseño de plantilla (&ast;.ifd)
* plantillas de salida (&ast;.mdf)
* archivos de datos (archivos &ast;.dat)
* archivos de preámbulo (archivos &ast;.pre)
* archivos de definición de datos (&ast;.tdf)

La siguiente configuración está disponible para el servicio Bridge de migración central.

**Directorio de instalación central:** El directorio donde está instalado Adobe Central 5.7.

## Configuración del servicio Conector del repositorio de contenido para Documentum de EMC {#content-repository-connector-for-emc-documentum-service-settings}

El servicio Content Repository Connector for EMC Documentum ( `EMCDocumentumContentRepositoryConnector`) permite crear procesos que interactúen con contenido almacenado en un repositorio de Documentum.

La siguiente configuración está disponible para el servicio Content Repository Connector for EMC Documentum.

**Ruta predeterminada del objeto Asset Link:** La parte predeterminada de la ruta en el repositorio de Documentum para almacenar el objeto Asset Link. La ruta real consiste en la ruta de acceso predeterminada y la ubicación de la plantilla de formulario en el repositorio de formularios de AEM.

Por ejemplo, si la ruta predeterminada está establecida en `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` y la plantilla de formulario está almacenada en una carpeta `/Docbase/forms/`, el objeto Asset Link se almacena en la siguiente ubicación:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

El valor predeterminado de esta configuración es `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Conector del repositorio de contenido para la configuración del servicio FileNet de IBM {#content-repository-connector-for-ibm-filenet-service-settings}

El Conector del repositorio de contenido para IBM FileNet permite crear procesos que interactúan con el contenido almacenado en un repositorio de IBM FileNet.

La siguiente configuración está disponible para el Conector del repositorio de contenido para el servicio FileNet de IBM.

**Ruta predeterminada del objeto Asset Link:** La parte predeterminada de la ruta en el repositorio FileNet de IBM para almacenar el objeto Asset Link. La ruta real consiste en la ruta de acceso predeterminada y la ubicación de la plantilla de formulario en el repositorio de formularios de AEM.

Por ejemplo, si la ruta predeterminada está establecida en `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` y la plantilla de formulario está almacenada en una carpeta `/Docbase/forms/`, el objeto Asset Link se almacena en la siguiente ubicación:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

El valor predeterminado de esta configuración es `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Convertir la configuración del servicio PDF {#convert-pdf-service-settings}

El servicio ConvertPDF ( `ConvertPdfService`) convierte los documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento de PDF en un archivo TIFF de varias páginas es práctico cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos de PDF.

Las siguientes configuraciones están disponibles para el servicio Convert PDF.

**Tipo de transacción:** Especifica cómo se debe propagar un contexto de transacción a una operación.

**Requerido:** Admite un contexto de transacción si existe uno; de lo contrario, se crea un nuevo contexto de transacción. Este es el valor predeterminado.

**Requiere nuevo:** Siempre crea un nuevo contexto de transacción. Si existe un contexto de transacción activo, se suspende.

**Tiempo de espera de transacción (en segundos):** El número de segundos que el proveedor de transacción subyacente debe esperar antes de revertir una transacción que está ajustando esta operación. Este valor se ignorará si se propaga un contexto de transacción existente. El valor predeterminado es 180.

**Resolución de umbral para el suavizado (en ppp):** Resolución de imagen por debajo de la cual se aplica el suavizado (o suavizado) al texto, las ilustraciones de líneas y las imágenes, si ha seleccionado las opciones &quot;Aplicar suavizado a&quot; para esos elementos.

**Aplicar suavizado al texto:** Controla el suavizado del texto. Para deshabilitar el suavizado del texto y hacer que el texto sea más nítido y fácil de leer con un ampliador de pantalla, desactive esta casilla de verificación.

**Aplicar suavizado a LineArt:** Aplica suavizado para eliminar ángulos abruptos en las líneas.

**Aplicar suavizado a las imágenes:** Aplica suavizado para minimizar los cambios abruptos en las imágenes.

## Configuración del servicio de Distiller {#distiller-service-settings}

El servicio Distiller (`DistillerService`) convierte los archivos PostScript, Encapsulated PostScript (EPS) y PRN en archivos PDF a través de una red.

Las siguientes configuraciones están disponibles para el servicio Distiller.

**Configuración de Adobe PDF:** Las siguientes opciones preconfiguradas se aplican al PDF generado:

* Impresión de alta calidad
* Páginas de gran tamaño
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* Calidad de prensa
* Tamaño de archivo más pequeño
* Estándar

Se pueden crear nuevas configuraciones a través de la interfaz de usuario de PDF Generator.

**Configuración de seguridad:** Configuración de seguridad preconfigurada que se aplica a los documentos de PDF generados. El valor predeterminado es Sin seguridad. Cree la configuración de seguridad mediante PDF Generator y, a continuación, introduzca la configuración aquí.

**Tamaño de grupo:** El tamaño inicial del grupo. Cuando se implementa el servicio Distiller, este número se utiliza para determinar el número de instancias de implementación del servicio que se crean y asignan al grupo libre a la espera de solicitudes de invocación. El contenedor de servicio puede responder inmediatamente a las solicitudes de invocación sin tener que inicializar primero una instancia de servicio.

## Configuración del servicio de Administración de documentos {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (Obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento del ciclo de vida del producto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

El servicio Administración de documentos (`DocumentManagementService`) habilita los procesos para que utilicen la funcionalidad de administración de contenido proporcionada por los servicios de contenido (obsoleto). Las operaciones de Administración de documentos proporcionan tareas básicas que son necesarias para mantener espacios y contenido en el sistema de administración de contenido. Algunos ejemplos de estas tareas son copiar, eliminar, mover, recuperar y almacenar contenido, crear espacios y asociaciones y obtener y establecer atributos de contenido.

Las siguientes configuraciones están disponibles para el servicio Administración de documentos.

**Esquema de almacenamiento:** Esquema del almacén en el que se encuentra el contenido. El valor predeterminado es Workspace.

**Puerto HTTP:** El puerto usado para acceder a Content Services (obsoleto). El valor predeterminado es 8080.

## Configuración del servicio de correo electrónico {#email-service-settings}

El correo electrónico se utiliza comúnmente para distribuir contenido o proporcionar información de estado como parte de un proceso automatizado. El servicio de correo electrónico (`EmailService`) permite a los procesos recibir mensajes de correo electrónico de un servidor POP3 o IMAP y enviar mensajes de correo electrónico a un servidor SMTP.

Por ejemplo, un proceso utiliza el servicio de correo electrónico para enviar un mensaje de correo electrónico con un archivo adjunto de formulario de PDF. El servicio de correo electrónico se conecta a un servidor SMTP para enviar el mensaje de correo electrónico con el archivo adjunto. El formulario de PDF está diseñado para permitir al destinatario hacer clic en Enviar después de completar el formulario. La acción hace que el formulario se devuelva como archivo adjunto al servidor de correo electrónico designado. El servicio de correo electrónico recupera el mensaje de correo electrónico devuelto y almacena el formulario completado en una variable de formulario de datos de proceso.

Las siguientes configuraciones están disponibles para el servicio de correo electrónico.

**Host SMTP:** Dirección IP o URL del servidor SMTP que se utilizará para enviar correo electrónico.

**Número de puerto SMTP:** El puerto usado para conectarse al servidor SMTP.

**Autenticar SMTP:** Seleccione si se requiere autenticación de usuario para conectarse al servidor SMTP.

**Usuario SMTP:** Nombre de usuario de la cuenta de usuario que se va a usar para iniciar sesión en el servidor SMTP.

**Contraseña SMTP:** La contraseña asociada a la cuenta de usuario SMTP.

**Seguridad de transporte SMTP:** Protocolo de seguridad que se utilizará para la conexión con el servidor SMTP:

* Seleccione Ninguno si no se utiliza ningún protocolo (los datos se envían sin cifrar)
* Seleccione SSL si utiliza el protocolo Secure Sockets Layer.
* Seleccione TLS si se utiliza la seguridad de la capa de transporte.

**Host POP3/IMAP:** Dirección IP o URL del servidor POP3 o IMAP que se va a utilizar para enviar correo electrónico.

**Nombre de usuario POP3/IMAP:** Nombre de usuario de la cuenta de usuario que se va a utilizar para iniciar sesión en el servidor POP3 o IMAP.

**Contraseña POP3/IMAP:** Contraseña asociada a la cuenta de usuario POP3 o IMAP.

**Número de puerto POP3/IMAP:** El puerto utilizado para conectarse al servidor POP3 o IMAP.

**POP3/IMAP:** Protocolo que se va a utilizar para enviar y recibir correo electrónico.

**Recibir seguridad de transporte:** El protocolo de seguridad que se va a usar para conectarse al servidor SMTP:

* Seleccione Ninguno si no se utiliza ningún protocolo (los datos se envían sin cifrar).
* Seleccione SSL si utiliza el protocolo Secure Sockets Layer.
* Seleccione TLS si se utiliza la seguridad de la capa de transporte.

## Configuración del servicio de cifrado {#encryption-service-settings}

El servicio Encryption (`EncryptionService`) permite cifrar y descifrar documentos. Cuando se encripta un documento, su contenido se vuelve ilegible. Un usuario autorizado puede desencriptar el documento para obtener acceso a su contenido. Si un documento PDF está encriptado con una contraseña, el usuario debe escribir la contraseña para abrir y visualizar el documento en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está encriptado con un certificado, el usuario debe desencriptar el documento PDF con la clave pública que corresponde al certificado (clave privada) que se utilizó para encriptarlo.

Los siguientes ajustes están disponibles para el servicio Encryption.

**Servidor LDAP predeterminado al que conectarse:** Nombre de host del servidor LDAP utilizado para recuperar certificados para el cifrado de documentos.

**Puerto LDAP predeterminado al que conectarse:** Número de puerto del servidor LDAP.

**Nombre de usuario LDAP predeterminado:** Si el servidor LDAP requiere autenticación, especifique el nombre de usuario que se utilizará para conectarse al servidor LDAP.

**Contraseña LDAP predeterminada:** Si el servidor LDAP requiere autenticación, especifique la contraseña que corresponde al nombre de usuario que se va a utilizar para conectarse al servidor LDAP.

>[!NOTE]
>
>Utilice la autenticación simple (nombre de usuario y contraseña) solo cuando la conexión esté protegida mediante SSL (mediante LDAPS).

<!-- **Compatibility Mode:**-->

## Configuración del servicio FTP {#ftp-service-settings}

El servicio FTP (`FTP`) permite que los procesos interactúen con un servidor FTP. Las operaciones del servicio FTP pueden recuperar archivos del servidor FTP, colocarlos en él y eliminarlos del servidor FTP. Por ejemplo, documentos como informes generados a partir de un proceso se pueden almacenar en un servidor FTP para su distribución. O un sistema externo puede generar algunos archivos basados en pasos anteriores de un proceso. En un paso posterior del proceso, los archivos se pueden transferir a una ubicación remota.

Los siguientes ajustes están disponibles para el servicio FTP.

**Host predeterminado:** Dirección IP o URL del servidor FTP.

**Puerto predeterminado:** El puerto usado para conectarse al servidor FTP. El valor predeterminado es 21.

**Nombre de usuario predeterminado:** Nombre de la cuenta de usuario que puede usar para tener acceso al servidor FTP. La cuenta de usuario debe tener privilegios suficientes para realizar las operaciones de FTP que requiere este servicio.

**Contraseña predeterminada:** Contraseña que se utilizará con el nombre de usuario especificado para autenticarse en el servidor FTP.

## Generar configuración del servicio de PDF {#generate-pdf-service-settings}

El servicio Generate PDF ( `GeneratePDFService`) convierte archivos en varios formatos nativos a documentos de PDF y convierte documentos de PDF a varios formatos de archivo.

Las siguientes configuraciones están disponibles para el servicio Generate PDF.

**Configuración de Adobe PDF:** Nombre de la configuración preconfigurada de Adobe PDF que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración de Adobe PDF se establece en la consola de administración, haciendo clic en Servicios > PDF Generator > Configuración de Adobe PDF. Esta configuración solo es aplicable a las conversiones basadas en PDFMaker.

**Configuración de seguridad:** Nombre de la configuración de seguridad preconfigurada que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración de seguridad se establece en la consola de administración, haciendo clic en Servicios > PDF Generator > Configuración de seguridad.

**Configuración de tipo de archivo:** Nombre de la configuración de tipo de archivo preconfigurada que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración del tipo de archivo se establece en la consola de administración, haciendo clic en Servicios > PDF Generator > Configuración del tipo de archivo.

**Usar WebCapture (sólo Windows):** Si esta configuración es verdadera, el servicio Generate PDF usa Acrobat para todas las conversiones de HTML a PDF. Esto puede mejorar la calidad de los archivos PDF producidos a partir de HTML, aunque el rendimiento puede ser ligeramente inferior. El valor predeterminado es False.

**Conversor principal para conversiones de HTML a PDF:** El servicio Generate PDF proporciona varias rutas para convertir archivos de HTML en documentos de PDF: Webkit, WebCapture (sólo Windows) y WebToPDF. Esta configuración permite al usuario seleccionar el convertidor principal para convertir HTML a PDF. De forma predeterminada, la opción WebToPDF está seleccionada.

**Conversor de reserva para conversiones de HTML a PDF:** Especifique el convertidor para conversiones de HTML a PDF si se produce un error en el convertidor principal. De forma predeterminada, la opción WebCapture (sólo Windows) está seleccionada.

**Usar la conversión de imágenes de Acrobat (solo Windows):** Si esta opción está establecida en true, el servicio Generate PDF usa Acrobat para todas las conversiones de imágenes a PDF. Esta configuración solo es útil si el mecanismo de conversión predeterminado de Java puro no puede convertir correctamente una proporción significativa de las imágenes de entrada. El valor predeterminado es False.

**Habilitar conversiones de AutoCAD basadas en Acrobat (solo Windows):** Si esta configuración es verdadera, el servicio Generate PDF usa Acrobat para todas las conversiones de DWG a PDF. Esta configuración sólo es útil si AutoCAD no está instalado en el servidor o si el mecanismo de conversión de AutoCAD no puede convertir archivos correctamente.

**Expresiones Regulares Para Averiguar La Oferta Especial Prohibida
Caracteres en el nombre de usuario (sólo Windows):** Especifica caracteres que interfieren con las operaciones de Export PDF y Optimizar PDF cuando aparecen en el nombre de un usuario.

**Tamaño del grupo ImageToPDF:** El tamaño del grupo del convertidor predeterminado (Java puro) de imagen a PDF en el servicio Generate PDF. Esta opción controla el número máximo de conversiones simultáneas de imagen a PDF que puede realizar el servicio Generate PDF. El valor predeterminado de esta configuración (recomendado para sistemas de un solo procesador) es 3, que se puede aumentar en sistemas de varios procesadores.

**Tamaño del grupo de HTML a PDF:** El tamaño del grupo del convertidor de HTML a PDF en el servicio Generate PDF. Esta opción controla el número máximo de conversiones simultáneas de HTML a PDF que puede realizar el servicio Generate PDF. El valor predeterminado de esta configuración (recomendado para sistemas de un solo procesador) es 3, que se puede aumentar en sistemas de varios procesadores.

**Tamaño del grupo de OCR:** El tamaño del grupo de PaperCaptureService que PDF Generator usa para OCR. El valor predeterminado de esta configuración (recomendado para sistemas de un solo procesador) es 3, que se puede aumentar en sistemas de varios procesadores. Esta configuración sólo es válida en sistemas Windows.

**Máximo de páginas de ImageToPDF en memoria para las conversiones de TIFF:** Esta configuración determina el número máximo de páginas de una imagen de TIFF que pueden permanecer en memoria antes de vaciarse en el disco durante la conversión a PDF. El valor predeterminado de esta configuración es 500, que se puede aumentar si se asigna memoria adicional al proceso de conversión de ImageToPDF.

**Familia de fuentes de reserva para las conversiones de HTML a PDF:** Nombre de la familia de fuentes que se utilizará en los documentos de PDF cuando la fuente utilizada en el HTML original no esté disponible para el servidor de AEM Forms. Especifique una familia de fuentes si espera convertir páginas de HTML que utilicen fuentes no disponibles. Por ejemplo, las páginas creadas en idiomas regionales podrían utilizar fuentes no disponibles.

**La lógica de reintento para conversiones nativas** rige los reintentos de generación de PDF si el primer intento de conversión ha fallado:

* **Sin reintento**

  No reintente la conversión de PDF si se ha producido un error en el primer intento de conversión

* **Reintentar**

  Reintentar la conversión de PDF independientemente de si se ha alcanzado el umbral de tiempo de espera. La duración de tiempo de espera predeterminada para el primer intento es 270 s.

* **Reintentar si el tiempo lo permite**

  Vuelva a intentar la conversión de PDF si el tiempo empleado para el primer intento de conversión fue inferior a la duración de tiempo de espera especificada. Por ejemplo, si la duración del tiempo de espera es de 270 segundos y el primer intento consumió 200 segundos, PDF Generator volverá a intentar la conversión. Si el primer intento consumió 270 segundos, no se volverá a intentar la conversión.

## Guías ES4 Utilidades configuración del servicio {#guides-es4-utilities-service-settings}

Al crear una guía, algunos recursos, como la definición de la guía, están incrustados en la guía. Los recursos también pueden existir como referencias a recursos de la aplicación almacenados localmente o en el servidor de AEM Forms. La Guía no contiene datos, y los valores de la ubicación de envío y las entradas no son adecuados para todos los entornos externos.

En la mayoría de los casos, los servicios de procesamiento predeterminados de las guías son suficientes para preparar una guía para usarla en Workspace u otros entornos externos. (En la vista Servicios, en Workbench, el servicio predeterminado es Guías (sistema)/Procesos/Guía de procesamiento - 1.0). El servicio Utilidades de guía (`GuidesUtility`) le permite crear un proceso personalizado para procesar una guía, si es necesario.

Las operaciones de Utilidades de la guía permiten añadir las siguientes tareas de renderización de la guía a un proceso:

* Determine si los datos están disponibles para rellenar la guía con
* Incrustar los datos de la guía o convertirlos en un vínculo
* Conversión del contenido referenciado en direcciones URL accesibles externamente
* Sustituya los valores de un documento de HTML u otro contenedor, o conviértalos en direcciones URL a las que se pueda acceder externamente
* Definición de la ubicación de envío
* Especificar valores de entrada
* Cree un parámetro para representar contenido referenciado
* Si hay variaciones disponibles, establezca una variación

Los valores predeterminados del servicio Utilidades de guía admiten la mayoría de los casos de uso. Sin embargo, si es necesario, puede cambiar los siguientes valores.

**publicPaths:** Esta opción ha quedado obsoleta. No utilice esta opción con formularios AEM Forms.

**pathInfoExpiryInSeconds:** Intervalo tras el cual caduca una solicitud de información de ruta de acceso de un cliente. El valor predeterminado es 1.

**garantíaExpiryInSeconds:** Intervalo después del cual caduca una solicitud de garantía de un cliente. El valor predeterminado es 315576000.

**mismatchExpiryInSeconds:** Intervalo tras el cual caduca una solicitud de garantía de un cliente, cuando la eTag (etiqueta de entidad) no coincide. (Una eTag es un encabezado de respuesta HTTP). El valor predeterminado es 1.

**guideContext:** Raíz de contexto de la aplicación web Guides. Coincide con el valor establecido mediante la aplicación web Guides. El valor predeterminado es /Guides/.

**secureRandomAlgorithm:** Algoritmo que se debe usar al generar claves e identificadores. Este valor se pasa al método getInstance de la clase Java SecureRandom. El valor predeterminado es SHA1PRNG.

**idBytes:** El número de bytes aleatorios que se utilizarán para un identificador de clave. El valor predeterminado es 6.

**macAlgorithm:** Algoritmo de MAC (código de autenticación de mensaje) que se utilizará para la verificación de URL de garantías. Este método se pasa al método getInstance de la clase Mac. El valor predeterminado es HmacSHA1.

**macRefreshIntervalInMinutes:** Cantidad de tiempo que una clave está activa. Cuando una clave ha estado activa para este intervalo, se genera una nueva clave. La nueva clave se convierte en la clave activa. La clave activa anteriormente se conserva durante el 10 % del intervalo de actualización. Este comportamiento permite que las direcciones URL que se generan mediante la clave antigua sigan funcionando a través del conmutador de claves. El valor predeterminado es 144000.

**macOverlapIntervalInMinutes:** Tiempo que la clave anterior seguirá siendo válida después de que se genere una nueva. El valor predeterminado es 1440 minutos (1 día).

**macKeySeed:** Un valor de inicialización para generar la dirección URL segura. Cuando esta opción está activada, la clave nunca se actualiza. Si se establece la misma semilla en diferentes servidores, estos generarán direcciones URL seguras compatibles. Esto puede resultar útil si hay varios servidores de Forms en uso detrás de un equilibrador de carga. Introduzca una secuencia aleatoria de caracteres y números como origen.

### Uso de guías en un clúster de servidores {#using-guides-in-a-server-cluster}

Al procesar una Guide en un clúster de servidores que no utiliza sesiones fijas, se produce un error con NullPointerException. Una solicitud de Guías utiliza direcciones URL seguras que, de forma predeterminada, son únicas para el servidor en el que se generan. En un clúster que utiliza sesiones fijas, después de que una solicitud llegue a un nodo del clúster, todas las solicitudes posteriores de esa sesión o usuario se enrutarán exclusivamente a ese servidor y todo estará bien. En un clúster que no utilice sesiones fijas, las solicitudes posteriores pueden alcanzar cualquier servidor del clúster. Si el servidor en el que se producen las solicitudes de visita no es el servidor original, no se puede resolver la dirección URL segura.

Si utiliza Guías en un clúster de servidores que no utiliza sesiones fijas, establezca el valor macKeySeed para el servicio GuidesUtility y, a continuación, detenga e inicie el clúster.

El valor macKeySeed es la semilla del generador de números aleatorios que se utiliza para generar las direcciones URL seguras. La configuración de este valor hace que cada nodo de clúster inicialice el generador de números aleatorios de la misma manera y tenga acceso a las mismas direcciones URL seguras. Puede utilizar cualquier cadena aleatoria para este valor semilla.

Cambie el valor de macKeySeed cuando necesite actualizar las direcciones URL seguras. La actualización de las direcciones URL seguras depende de la directiva de seguridad y es similar a la directiva de actualización para cambiar la contraseña de la raíz maestra del servidor. macSeedValue es análogo a la contraseña maestra para las URL seguras, ya que se utiliza para generar un nuevo número aleatorio único para utilizarlo en la generación y recuperación de URL seguras.

Reinicie el clúster porque macSeedValue es de solo lectura al iniciar el sistema. Es necesario reiniciar todos los nodos para leer el valor, ya que lo utilizan de forma independiente para inicializar sus números aleatorios internos con el valor semilla.

## Configuración del servicio JDBC {#jdbc-service-settings}

El servicio JDBC (`JdbcService`) permite que los procesos interactúen con las bases de datos.

La siguiente configuración está disponible para el servicio JDBC.

**datasourceName:** Valor de cadena que representa el nombre JNDI del origen de datos que se va a utilizar para conectarse al servidor de base de datos. El origen de datos debe definirse en el servidor de aplicaciones que aloja el servidor de Forms. El valor predeterminado es el nombre JNDI del origen de datos de la base de datos de formularios AEM Forms.

## Configuración del servicio JMS {#jms-service-settings}

El servicio JMS ( `JMS`) habilita la interacción con proveedores de Java Messaging System (JMS) que implementan la mensajería punto a punto y la mensajería de publicación/suscripción.

Configure el servicio JMS con propiedades predeterminadas para que las operaciones del servicio puedan conectarse e interactuar con un proveedor JMS y un servicio JNDI asociado. Los valores de las propiedades del servicio se establecen en valores predeterminados basados en el servidor de aplicaciones JBoss. Cambie estos valores si utiliza un servidor de aplicaciones diferente para alojar formularios AEM.

Las siguientes configuraciones están disponibles para el servicio JMS.

**Dirección URL del proveedor:** Dirección URL del proveedor de servicios JNDI. El valor predeterminado se basa en el servidor de aplicaciones JBoss. Las siguientes direcciones URL son valores predeterminados para los servidores de aplicaciones compatibles con los formularios AEM Forms:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nombre de usuario JNDI:** Nombre de usuario de la cuenta que se va a utilizar para autenticarse con el proveedor de servicios JNDI que se utiliza para buscar nombres de temas y colas. El valor predeterminado es invitado.

**Contraseña JNDI:** La contraseña asociada al nombre de usuario especificado para el nombre de usuario JNDI. El valor predeterminado es invitado.

**Fábrica de contexto inicial:** La clase Java que se va a utilizar como fábrica de contexto inicial. El servicio JMS utiliza esta clase para crear un contexto inicial, que es el punto de partida para resolver nombres de temas y colas. El valor predeterminado es la fábrica de contexto inicial para el servicio JMS en JBoss. Las siguientes clases son las fábricas de contexto iniciales para los servidores de aplicaciones compatibles con los formularios AEM Forms:

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.namespace.WsnInitialContextFactory

**Nombre de usuario de conexión:** La contraseña asociada al nombre de usuario especificado para el Nombre de usuario de conexión. El valor predeterminado es invitado.

**Contraseña de conexión:** La contraseña asociada al nombre de usuario especificado para el nombre de usuario de conexión. El valor predeterminado es invitado.

**Otras propiedades:** Pares de nombre y valor de propiedad que puede pasar al proveedor de servicios JNDI. Estas propiedades dependen de la implementación y configuración del proveedor que utilice.

Los pares de nombre y valor de la propiedad están separados por punto y coma **;**. Por ejemplo, el siguiente texto muestra el valor que se especificaría para dos propiedades denominadas name1 y name2, con valores value1 y value2, respectivamente:

`name1=value1;name2=value2`

## Configuración del servicio LDAP {#ldap-service-settings}

El servicio LDAP (`LDAPService`) proporciona operaciones para consultar directorios LDAP. Los directorios LDAP se utilizan generalmente para almacenar información sobre las personas, los grupos y los servicios de una organización.

Las siguientes configuraciones están disponibles para el servicio LDAP.

**Fábrica de contexto inicial:** La clase Java que se va a utilizar como fábrica de contexto. Esta clase se utiliza para crear una conexión con el servidor LDAP. El valor predeterminado es com.sun.jndi.ldap.LdapCtxFactory, que es adecuado para la mayoría de los servidores LDAP.

**Dirección URL del proveedor:** Dirección URL que se va a utilizar para conectarse al servicio LDAP. El formato del valor es `ldap://server name:port`

*nombre de servidor* es el nombre del equipo que hospeda el servidor LDAP

*puerto* es el puerto de comunicaciones que utiliza el servicio LDAP. El valor predeterminado es 389, que es el puerto estándar utilizado para las conexiones LDAP.

**Nombre de usuario:** Nombre de usuario de la cuenta de usuario que se va a utilizar para iniciar sesión en el servidor LDAP. La cuenta de usuario debe tener permiso para conectarse al servidor y leer la información del directorio LDAP.

Según el servidor LDAP, el nombre de usuario podría ser un nombre de usuario simple como `myname` o un DN, como `cn=myname,cn=users,dc=myorg`.

**Contraseña:** Contraseña que corresponde al nombre de usuario proporcionado para la configuración de nombre de usuario.

**Otras propiedades:** Valor de cadena que representa otras propiedades y sus valores correspondientes que puede proporcionar al servidor LDAP. El valor tiene el siguiente formato:

`property=value;property=value;...`

## Ajustes del servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)` le permite especificar credenciales para el usuario de formularios AEM que tiene permisos de suplantación. Para obtener información acerca de los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Los siguientes ajustes están disponibles para el servicio de configuración de Microsoft SharePoint:

* Nombre de usuario para un usuario con permisos de suplantación
* Contraseña del usuario anterior

**Habilitar SSL (HTTPS):**

**Tiempo de vida:** Tiempo, en segundos, que este perfil de aprovisionamiento es válido y se almacena en caché en el cliente. El valor predeterminado es 86400 (24 horas). Cuando una aplicación cliente se sincroniza con el servidor y ha transcurrido la cantidad de tiempo especificada, la aplicación cliente solicita un nuevo perfil de aprovisionamiento del servidor.

**Cifrado:** Especifica si se deben cifrar los datos almacenados en el dispositivo móvil.

**Aplicación Forms:** Habilita la característica Forms en las aplicaciones cliente móviles. Cuando se selecciona esta opción, los usuarios pueden abrir formularios e iniciar procesos desde sus dispositivos móviles.

**Aplicación Tasks:** habilita la característica Tasks en las aplicaciones cliente móviles. Cuando se selecciona esta opción, los usuarios pueden acceder a sus listas de tareas y completar tareas desde sus dispositivos móviles.

**Aplicación de servicios de contenido:** Habilita la característica Servicios de contenido en la aplicación cliente móvil. Esta función solo está disponible para iOS. Si se selecciona esta opción, los usuarios de iPhone y iPad pueden acceder a los archivos almacenados en el servidor WebDAV de su organización.

**Compatibilidad sin conexión:** Permite a los usuarios seguir usando las aplicaciones cliente móviles incluso cuando no tienen conexión con el servidor (por ejemplo, cuando están fuera del intervalo de celdas o en modo avión). Los usuarios también deben habilitar la configuración Compatibilidad con conexión en sus dispositivos móviles. Esta función está disponible para dispositivos Android y iOS. Esta función está desactivada de forma predeterminada.

>[!NOTE]
>
>Si se ha habilitado la compatibilidad sin conexión y, a continuación, la deshabilita, los perfiles de aprovisionamiento de los usuarios se actualizan inmediatamente o en cuanto están en línea. Si un usuario ha estado trabajando sin conexión, todas las tareas pendientes se devuelven a su lista Tareas y todos los elementos de su Cola, incluidos los formularios pendientes, las tareas y los formularios que contienen errores de validación, se eliminan de la Cola.

**Android:** permite que los dispositivos Android se conecten al servidor.

**Apple iOS:** permite que los iPhones y los iPads se conecten al servidor.

**AIR:** permite que los dispositivos que ejecutan aplicaciones basadas en Adobe AIR® se conecten al servidor.

**BlackBerry:** permite que los dispositivos BlackBerry se conecten al servidor.

**Se requiere Android Microsoft Exchange ActiveSync:** Especifica si el administrador de directivas de Microsoft Exchange ActiveSync (EAS) debe estar instalado y activo en los dispositivos Android. Si se selecciona esta opción, el EAS debe aplicarse en el dispositivo Android. Cuando esta opción no está seleccionada, no se realiza ninguna comprobación, aunque siguen aplicándose otros requisitos.

**Longitud mínima del PIN de Android:** Los dispositivos Android deben tener una configuración global que exija que el PIN o la contraseña tengan al menos esta longitud. No basta con tener un PIN de la longitud especificada. El sistema debe aplicar la longitud del PIN para que los usuarios no puedan quitarlo ni acortarlo más tarde. El valor predeterminado es 4.

**Máximo de reintentos de contraseña de Android antes del borrado:** Los dispositivos Android tienen una configuración global que borra el sistema después de un número especificado de intentos de contraseña no válidos. Esta configuración global está habilitada y es igual o inferior al valor especificado aquí. El valor predeterminado es 5.

**Borrar Android al quitar:** Especifica lo que sucede cuando se produce una infracción de directiva en un dispositivo Android. Cuando se selecciona esta opción, se elimina la cuenta. Cuando esta opción no está seleccionada, se eliminan la contraseña de la cuenta almacenada y los datos almacenados en caché. No se realizan más intentos de sincronización hasta que el usuario corrige la infracción de directiva.

## Configuración del servicio de salida {#output-service-settings}

El servicio Output `(OutputService)` le permite combinar datos de formulario XML con un diseño de formulario creado en AEM Forms Designer para crear una secuencia de salida de documento en uno de los siguientes formatos:

* Flujo de salida de documento de PDF o PDF/A.
* Un flujo de salida de Adobe PostScript.
* Una secuencia de salida de Lenguaje de control de impresora (PCL).
* Un flujo de salida Zebra Programming Language (ZPL).

El flujo de salida se puede enviar a una impresora de red, a una impresora local o a un archivo de disco. Cuando se utiliza el servicio Output como parte de un proceso, también se puede enviar el flujo de salida a un destinatario de correo electrónico como archivo adjunto.

Los siguientes ajustes están disponibles para el servicio Output.

**Tipo de transacción:** Especifica cómo se debe propagar un contexto de transacción a una operación:

**Requerido:** admite un contexto de transacción si ya existe uno; de lo contrario, se crea un nuevo contexto de transacción. Este es el valor predeterminado.

**Requiere nuevo:** Siempre crea un nuevo contexto de transacción. Si existe un contexto de transacción activo, se suspende.

**Tiempo de espera de transacción (en segundos):** El número de segundos que el proveedor de transacciones subyacente espera antes de revertir una transacción que está ajustando esta operación. Este valor se ignora si se propaga un contexto de transacción existente.

Al procesar archivos de datos de gran tamaño o trabajar en un servidor ocupado, puede ser necesario aumentar el tiempo de espera del servicio Output. Para cambiar el valor de tiempo de espera, asegúrese de que los servidores de hardware tengan memoria adecuada y de que la memoria esté disponible para el montón de Java Application Server. El valor predeterminado es `180`.

## Configuración del servicio de configuración PDFG {#pdfg-config-service-settings}

Las siguientes opciones de configuración están disponibles para el servicio de configuración de PDFG ( `PDFGConfigService`).

**Directorio de opciones de trabajos de usuario:** Ruta de acceso a la carpeta del sistema de archivos donde el servicio c escribe los archivos de opciones de trabajo a los que Acrobat Pro Extended tiene acceso. El valor predeterminado es [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**Directorio de inicio de PS:** Ruta de acceso a la carpeta del sistema de archivos donde se guardan los archivos de inicio requeridos por Adobe Acrobat Distiller. El valor predeterminado es [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**Archivo de inicio de PS:** Nombre del archivo de inicio requerido por Adobe Acrobat Distiller. El valor predeterminado es example.ps.

**Tiempo de espera de conversión del servidor:** Tiempo de espera máximo de conversión del trabajo (en segundos) para el servicio Generate PDF y el servicio Distiller. Esta configuración limita el tiempo de espera máximo de conversión que se puede especificar en el archivo config.xml y en las páginas de la consola de administración de PDF Generator. El valor predeterminado es 270.

**Tiempo de espera global del servidor:** Mientras se realizan las conversiones de PDF, un servidor de Forms tiene en cuenta el límite de tiempo de espera. Configure el valor timeout para resolver el problema.

**Prefijo de opciones de trabajo:** Prefijo utilizado por el servicio Generate PDF para anteponer una cadena corta a los archivos de opciones de trabajo que crea temporalmente para su uso en Acrobat Distiller. El valor predeterminado es pdfg.

**Aplicaciones no Unicode:** Lista separada por comas de nombres de aplicaciones que se sabe que no admiten Unicode. Esta lista se rellena previamente con los nombres de varias aplicaciones, cuya compatibilidad está preconfigurada en PDF Generator. Si decide añadir compatibilidad con las conversiones de PDF a través de otras aplicaciones de terceros que no admiten Unicode, debe añadirlas a esta lista. El valor predeterminado es Autocad, Excel, PowerPoint, Project, Publisher, Visio, Word y WordPerfect.

**Recuento de grupos de subprocesos del servidor:** controla el tamaño del grupo de subprocesos que el servicio Generate PDF utiliza internamente para atender las solicitudes de conversión de HTML a PDF que implican el uso de arañas (conversión de páginas vinculadas accesibles desde la página principal). El valor predeterminado es 20.

**Segundos del análisis de limpieza de PDFG:** Consulte la sección Segundos de caducidad del trabajo para obtener más información.

**Segundos de caducidad del trabajo:** El servicio Generate PDF elimina los archivos de entrada en cuanto se convierten. Almacena los archivos de salida temporalmente durante un periodo determinado por la configuración Segundos del análisis de limpieza de PDF Generator y Segundos de caducidad del trabajo.

La configuración Segundos de caducidad del trabajo especifica la antigüedad de un archivo o carpeta vacía antes de que pueda eliminarse. La configuración Segundos del análisis de limpieza de PDF Generator especifica la frecuencia con la que un subproceso de limpieza analiza las carpetas temporales en busca de archivos que se pueden eliminar.

Por ejemplo, si Segundos de caducidad del trabajo se establece en 100 y Segundos del análisis de limpieza de PDFG se establece en 200, el subproceso de limpieza se ejecuta cada 200 segundos y elimina los archivos que tengan 100 segundos o más.

El valor predeterminado de Segundos del análisis de limpieza de PDF Generator es `43200` (12 horas). El valor predeterminado de Segundos de caducidad del trabajo es `86400` (24 horas).

**Configuración regional predeterminada:** Se usa para anular la configuración regional predeterminada (país + idioma) del servidor donde se implementa el servicio Generate PDF. Si no se especifica este parámetro, la configuración regional predeterminada se determina a partir del sistema operativo en el que se implementa el servicio. Este parámetro controla el idioma en el que se devuelven los mensajes de error a las API.

## Configuración del servicio de servicios de datos del flujo de trabajo Forms {#forms-workflow-data-services-service-settings}

Los siguientes servicios amplían los servicios de datos y exponen ensambladores que Workspace utiliza para hablar con el servidor. No cambie las opciones de configuración de estos servicios a menos que el Soporte técnico de Adobe se lo indique. Estos servicios no están destinados al acceso directo:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Configuración del servicio remoto {#remoting-service-settings}

La mayoría de los servicios están configurados para que pueda acceder a ellos a través de (obsoleto para formularios AEM) Remoting de formularios AEM. Para obtener información sobre la comunicación remota de formularios AEM Forms (obsoleta en formularios AEM Forms), consulte [Programar con formularios AEM Forms](https://adobe.com/go/learn_aemforms_programming_63).

Los siguientes ajustes están disponibles para el servicio Remoting.

**Método de autenticación de cliente de Flex:** Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas. Elija entre Personalizado o Básico. El valor predeterminado es Básico.

**Permitir la serialización de clases no serializables:** La mayoría de los extremos de los formularios AEM permiten que solo se usen clases serializables para la invocación. En versiones anteriores, el extremo remoto permitía que se utilizaran clases no serializables para la invocación desde clientes basados en Flex. Se ha cambiado para evitar una vulnerabilidad de seguridad descrita en APS11-15. Si desea seguir utilizando clases no serializables con el extremo de comunicación remota de Flex, active esta casilla de verificación.

## Configuración del servicio de repositorio {#repository-service-settings}

El servicio de repositorio ( `RepositoryService`) proporciona servicios de administración y almacenamiento de recursos a los formularios de AEM. Cuando los desarrolladores crean una aplicación, pueden implementar los recursos en el repositorio en lugar de en un sistema de archivos. Los recursos pueden incluir cualquier tipo de material colateral, incluidos formularios XML, PDF forms (incluidos formularios Acrobat), fragmentos de formulario, imágenes, perfiles, directivas, archivos SWF, archivos DDX, esquemas XML, archivos WSDL y datos de prueba.

Puede utilizar el repositorio predeterminado incluido con los formularios de AEM o utilizar un repositorio de terceros (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager).

El servicio Proveedor de repositorio es un delegado de servicio que actúa como interfaz para un servicio de proveedor. Esto le permite conectarse a una API común y no tiene que saber qué servicio de proveedor implementa las capacidades de almacenamiento. El servicio Proveedor de repositorios proporciona almacenamiento de base de datos para los recursos del servicio de repositorio.

La siguiente configuración está disponible para el servicio Repositorio.

**Servicio de proveedor:** Nombre del servicio que se usa como proveedor de almacenamiento. El valor predeterminado es RepositoryProviderService.

## Configuración del servicio de firma {#signature-service-settings}

El servicio Signature ( `SignatureService`) permite a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que los documentos no se modifiquen. Al modificar un documento, se rompe su firma. Debido a que las funciones de seguridad se aplican al propio documento, éste permanece seguro y controlado durante todo su ciclo de vida; más allá del cortafuegos, cuando se descarga sin conexión y cuando se devuelve a su organización.

Los siguientes ajustes están disponibles para el servicio Signature.

**Nombre del servicio SPI de HSM remoto:** Esta opción está destinada a utilizarse cuando el HSM está instalado en un equipo remoto. Especifique esta opción cuando los formularios AEM Forms estén instalados en un sistema Windows de 64 bits y utilice dispositivos HSM para firmar.

**URL del servicio web HSM remoto:** Especifique esta opción cuando los formularios AEM Forms estén instalados en Windows de 64 bits y esté usando dispositivos HSM para firmar.

**Certificación para incluir cambios en la carga de formularios:** Cuando se selecciona esta opción, el estado del formulario XFA se certifica además de la plantilla XFA. Tenga en cuenta que habilitar esta opción puede tener un impacto negativo en el rendimiento. El valor predeterminado es True.

**Ejecutar scripts de Document JavaScript:** Especifica si se ejecutarán scripts de Document JavaScript durante operaciones de firma. El valor predeterminado es False.

**Procesar documentos con compatibilidad con Acrobat 9:** Especifica si se habilita la compatibilidad con Acrobat 9. Por ejemplo, cuando se selecciona esta opción, se habilita Certificación visible en archivos PDF dinámicos. El valor predeterminado es False.

**Incrustar información de revocación al firmar:** Especifica si la información de revocación está incrustada al firmar el documento de PDF. El valor predeterminado es False.

**Incrustar información de revocación al certificar:** Especifica si la información de revocación está incrustada al certificar el documento de PDF. El valor predeterminado es False.

**Aplicar incrustación de información de revocación para todos los certificados
Durante la firma o certificación:** Especifica si una operación de firma o certificación falla si no está incrustada la información de revocación válida para todos los certificados. Tenga en cuenta que si un certificado no contiene información de CRL u OCSP, se considera válido, incluso si no se recupera ninguna información de revocación. El valor predeterminado es False.

**Orden de comprobación de revocación:** Especifica el orden de comprobación de revocación cuando es posible realizar la comprobación mediante los mecanismos Lista de revocación de certificados (CRL) y Protocolo de estado de certificado en línea (OCSP). El valor predeterminado es OCSPFirst.

**Tamaño máximo de la información de archivo de revocación:** Tamaño máximo de la información de archivo de revocación en kilobytes. Los formularios AEM Forms intentan almacenar la mayor cantidad de información de revocación posible sin superar el límite. El valor predeterminado es 10 KB.

**Firmas De Soporte Creadas A Partir De Compilaciones Previas Al Lanzamiento De
Productos Adobe:** Si se selecciona esta opción, la firma creada con la versión preliminar de los productos Adobe se validará correctamente. El valor predeterminado es False.

**Opción de tiempo de comprobación:** Especifica la hora de verificación del certificado de un firmante. El valor predeterminado es Proteger hora actual u otra hora.

**Usar información de revocación archivada en la firma durante
Validación:** Especifica si la información de revocación archivada con la firma se usa para la comprobación de revocación. El valor predeterminado es True.

**Usar Información De Validación Almacenada En El Documento Para
Validación de firmas:** Si se selecciona esta opción, se utiliza la información de validación (incluida la información de revocación y de marca de tiempo) incrustada en el documento para validar firmas. El valor predeterminado es True.

**Máximo de sesiones de verificación anidadas permitidas:** Número máximo de sesiones de verificación anidadas permitidas. Los formularios de AEM utilizan este valor para evitar un bucle infinito al comprobar los certificados del firmante de OCSP o CRL cuando el certificado de OCSP o CRL no está configurado correctamente. El valor predeterminado es 10.

**Desviación máxima del reloj para la verificación:** Tiempo máximo, en minutos, que puede ser posterior al tiempo de validación. Si la desviación del reloj es mayor que este valor, la firma no será válida. El valor predeterminado es 65 minutos.

**Caché de duración del certificado:** Duración de un certificado, recuperado en línea o por otros medios, en la caché. El valor predeterminado es 1 día.

### Opciones de transporte {#transport-options}

**Host proxy:** La dirección URL del host proxy. Se utiliza solo si se proporciona algún valor válido. No hay valor predeterminado.

**Puerto Proxy:** El puerto proxy. Escriba cualquier número de puerto válido de 0 a 65535. El valor predeterminado es 80.

**Nombre de usuario de inicio de sesión de proxy:** Nombre de usuario de inicio de sesión de proxy. Solo se usa si se proporciona algún valor válido para el host y el puerto proxy. No hay valor predeterminado.

**Contraseña de inicio de sesión de proxy:** Contraseña de inicio de sesión de proxy. Solo se usa si se proporciona algún valor válido para el host proxy, el puerto proxy y el nombre de usuario de inicio de sesión proxy. No hay valor predeterminado.

**Límite máximo de descarga:** Cantidad máxima de datos, en MB, que se pueden recibir por conexión. El valor mínimo es 1 MB y el valor máximo es 1024 MB. El valor predeterminado es 16 MB.

**Tiempo de espera de conexión:** Tiempo máximo de espera, en segundos, para establecer una nueva conexión. El valor mínimo es 1 y el valor máximo es 300. El valor predeterminado es 5.

**Tiempo de espera de socket:** Tiempo máximo de espera, en segundos, antes de que se agote el tiempo de espera de un socket (mientras se espera la transferencia de datos). El valor mínimo es 1 y el valor máximo es 3600. El valor predeterminado es 30.

### Opciones de validación de rutas {#path-validation-options}

**Requerir directiva explícita:** Especifica si la ruta de acceso debe ser válida para al menos una de las directivas de certificado asociadas al anclaje de confianza del certificado del firmante. El valor predeterminado es False.

**Inhibir CUALQUIER directiva:** Especifica si el identificador de objeto de directiva (OID) debe procesarse si se incluye en un certificado. El valor predeterminado es False.

**Inhibir asignación de directiva:** Especifica si se permite la asignación de directiva en la ruta de certificación. El valor predeterminado es False.

**Comprobar todas las rutas:** Especifica si todas las rutas deben validarse o si la validación debe detenerse después de encontrar la primera ruta válida. Seleccione true o false. El valor predeterminado es False.

**Servidor LDAP:** Servidor LDAP utilizado para buscar certificados para la validación de rutas. No hay valor predeterminado.

**Seguir URI en el AIA de certificado:** Especifica si los identificadores uniformes de recursos (URI) del AIA de certificado se procesan durante la detección de rutas. El valor predeterminado es False.

**Se requiere la extensión de restricciones básicas en los certificados de CA:** Especifica si la extensión de certificado de restricciones básicas de la entidad de certificación (CA) debe estar presente para los certificados de CA. Algunos de los primeros certificados raíz certificados alemanes (7 y anteriores) no cumplen con RFC 3280 y no contienen la extensión de restricción básica. Si se sabe que el certificado EE de un usuario se encadena a una raíz alemana de este tipo, anule la selección de esta casilla de verificación. El valor predeterminado es True.

**Requerir firma de certificado válida durante la generación de cadenas:** Especifica si el generador de cadenas requiere firmas válidas en los certificados utilizados para generar cadenas. Cuando se activa esta casilla de verificación, el generador de cadenas no generará cadenas con firmas RSA no válidas en los certificados. Considere la cadena CA > ICA > EE donde la firma de la CA en una ICA no es válida. Si esta configuración es verdadera, el edificio de cadenas se detendrá en el ICA y el CA no se incluirá en la cadena. Si esta configuración es falsa, se genera la cadena de certificados de 3 certificados completa. Esta configuración no afecta a las firmas DSA. El valor predeterminado es False.

### Opciones del proveedor de marcas de hora {#timestamp-provider-options}

**URL de servidor TSP:** URL del proveedor de marca de tiempo predeterminado. Se utiliza solo si se proporciona algún valor válido. No hay valor predeterminado.

**Nombre de usuario del servidor TSP:** El nombre de usuario si lo necesita el proveedor de marcas de tiempo. Se utiliza solo si se proporciona algún valor válido para la dirección URL. No hay valor predeterminado.

**Contraseña del servidor TSP:** La contraseña del nombre de usuario anterior si es necesario por el proveedor de marca de tiempo. Se utiliza solo si se proporciona algún valor válido para la dirección URL y el nombre de usuario. No hay valor predeterminado.

**Algoritmo hash de solicitud:** Especifica el algoritmo hash que se utilizará al crear la solicitud para el proveedor de marca de tiempo. El valor predeterminado es SHA1.

**Estilo de comprobación de revocación:** Especifica el estilo de comprobación de revocación utilizado para determinar el estado de confianza del certificado del proveedor de marca de tiempo a partir de su estado de revocación observado. El valor predeterminado es Mejor esfuerzo.

**Enviar cadena nonce:** Especifica si se envía una cadena nonce con la solicitud del proveedor de marca de tiempo. Un nonce puede ser una marca de tiempo, un contador de visitas en una página web o un marcador especial destinado a limitar o evitar la reproducción o reproducción no autorizada de un archivo. El valor predeterminado es True.

**Usar marcas de hora caducadas durante la validación:** Si se selecciona esta opción, se pueden usar marcas de hora caducadas para recuperar las horas de validación de las firmas. El valor predeterminado es True.

**Tamaño de respuesta TSP:** Tamaño estimado, en bytes, de la respuesta TSP. Este valor debe representar el tamaño máximo de la respuesta de marca de tiempo que el proveedor de marca de tiempo configurado podría devolver. No cambie esto a menos que esté absolutamente seguro. El valor mínimo es 60B y el valor máximo es 10240B. El valor predeterminado es 4096B.

**Omitir extensión de servidor TimeStamp**: seleccione la opción **Omitir extensión de servidor TimeStamp** para evitar que el servidor de AEM Forms se ponga en contacto con el servidor de marca de hora especificado. La selección de la opción ayuda a evitar errores de proceso que se producen debido al tiempo de espera de conexión entre AEM Forms y los servidores de marca de hora.

### Opciones de lista de revocación de certificados {#certificate-revocation-list-options}

**Consultar primero el URI local:** Especifica si la ubicación de CRL proporcionada en el URI local o en la búsqueda de CRL debe tener preferencia sobre cualquier ubicación especificada dentro de un certificado con el fin de comprobar la revocación. El valor predeterminado es False.

**URI local para búsqueda de CRL:** URL del proveedor de CRL local. Este valor solo se consulta si la configuración Consultar URI local primero está establecida en verdadero. No hay valor predeterminado.

**Estilo de comprobación de revocación:** Especifica el estilo de comprobación de revocación utilizado para determinar el estado de confianza del certificado del proveedor de CRL a partir de su estado de revocación observado. El valor predeterminado es Mejor esfuerzo.

**Servidor LDAP para búsqueda de CRL:** Servidor LDAP utilizado para obtener las CRL (como www.ldap.com). Todas las consultas basadas en DN para CRL se dirigirán a este servidor. No hay valor predeterminado.

**Conectarse:** Especifica si se conecta para obtener una CRL. Si es false, solo se consultan las CRL en caché (en el disco local o las incrustadas con la firma). El valor predeterminado es True.

**Ignorar fechas de validez:** Especifica si se deben ignorar las horas thisUpdate y nextUpdate de la respuesta, lo que impide que estos tiempos tengan un efecto negativo en la validez de la respuesta. El valor predeterminado es False.

**Requerir extensión AKI en CRL:** Especifica si la extensión Identificador de clave de entidad emisora debe incluirse en una CRL. El valor predeterminado es False.

### Opciones de protocolo de estado de certificado en línea {#online-certificate-status-protocol-options}

**URL del servidor OCSP:** URL del servidor OCSP predeterminado. El uso del servidor OCSP especificado mediante esta dirección URL depende de la configuración de la opción URL a consultar. No hay valor predeterminado.

**Opción URL a consultar:** Controla la lista y el orden de los servidores de OCSP que se usan para realizar la comprobación de estado. El valor predeterminado es UseAIAInCert.

**Estilo de comprobación de revocación:** Especifica el estilo de comprobación de revocación que se usa al comprobar el certificado del servidor OCSP. El valor predeterminado es CheckIfAvailable.

**Enviar número:** Especifica si se envía un número con la solicitud de OCSP. Un nonce puede ser una marca de tiempo, un contador de visitas en una página web o un marcador especial destinado a limitar o evitar la reproducción o reproducción no autorizada de un archivo. El valor predeterminado es True.

**Tiempo máximo de sesgo del reloj:** Desviación máxima permitida, en minutos, entre el tiempo de respuesta y la hora local. El valor mínimo es 0 y el valor máximo es 2147483647 m. El valor predeterminado es 5 m.

**Tiempo de actualización de la respuesta:** Tiempo máximo, en minutos, para el que una respuesta OCSP preconstruida se considera válida. El valor mínimo es 1 m y el valor máximo permitido es 2147483647. El valor predeterminado es 525600 (un año).

**Firmar solicitud de OCSP:** Especifica si se debe firmar la solicitud de OCSP. El valor predeterminado es False.

**Alias de credencial de firmante de solicitud:** Especifica el alias de credencial que se utilizará para firmar la solicitud de OCSP si la firma está habilitada. Solo se utiliza si la firma de la solicitud de OCSP está habilitada. No hay valor predeterminado.

**Conectarse:** Especifica si se conecta para realizar la comprobación de revocación. El valor predeterminado es True.

**Ignorar las horas thisUpdate y nextUpdate de la respuesta:** Especifica si se deben ignorar las horas thisUpdate y nextUpdate de la respuesta, lo que impide que estos tiempos tengan un efecto negativo en la validez de la respuesta. El valor predeterminado es False.

**Permitir extensión OCSPNoCheck:** Especifica si la extensión OCSPNoCheck está permitida en el certificado de firma de respuesta. El valor predeterminado es True.

**Requerir extensión CertHash OCSP ISIS-MTT:** Especifica si se debe incluir una extensión hash de clave pública de certificado en las respuestas OCSP. El valor predeterminado es False.

### Opciones de control de errores para depuración {#error-handling-options-for-debugging}

**Purgar caché de certificados en la siguiente llamada de API:** Especifica si se purgará la caché de certificados cuando se realice la siguiente operación de servicio de firma. Una vez realizada la operación, esta opción se vuelve a establecer en false. El valor predeterminado es False.

**Purgar caché de CRL en la siguiente llamada de API:** Especifica si se purga la caché de CRL cuando se llama a la siguiente operación de servicio de firma. Una vez realizada la operación, esta opción se vuelve a establecer en false. El valor predeterminado es False.

**Purgar la caché de OCSP en la siguiente llamada de API:** Especifica si se purgará la caché de OCSP cuando se realice la siguiente operación de servicio de firma. Una vez realizada la operación, esta opción se vuelve a establecer en false. El valor predeterminado es False.

## Configuración del servicio de carpetas inspeccionadas {#watched-folder-service-settings}

El servicio de carpetas inspeccionadas (`WatchedFolder`) configura atributos que son comunes para todos los extremos de carpetas inspeccionadas. También proporciona valores predeterminados para los extremos de carpeta observados. (Consulte [Configuración de puntos finales de carpetas vigiladas](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) No es invocado por aplicaciones cliente externas ni se utiliza en procesos creados en Workbench.

Las siguientes configuraciones están disponibles para el servicio de carpetas inspeccionadas.

**Expresión cron:** La expresión cron utilizada por quartz para programar el sondeo del directorio de entrada.

**Recuento de repeticiones:** El número de veces que se sondea el directorio de entrada. Recuento de repetición predeterminado que se utilizará si este valor no se especifica en la configuración del extremo. El valor -1 indica un análisis indefinido del directorio. El valor predeterminado es -1.

**Intervalo de repetición:** El número predeterminado en segundos entre cada sondeo. Este valor se utiliza como intervalo de repetición a menos que se especifique un valor diferente en la configuración del extremo de la carpeta vigilada. El valor predeterminado es 5. Consulte la descripción de la configuración del tamaño del lote para obtener más información.

**Asincrónica:** Identifica el tipo de invocación como asincrónico o sincrónico. Los procesos transitorios y sincrónicos solo se pueden invocar sincrónicamente. El valor predeterminado es asíncrono.

**Tiempo de espera:** El valor predeterminado de tiempo, en segundos, tras el cual se recuperarán los archivos de las carpetas de entrada. Si el archivo o la carpeta es anterior al tiempo especificado en el tiempo de espera, se recoge para su procesamiento. El valor predeterminado es 0.

**Tamaño de lote:** El valor predeterminado para el número de archivos o carpetas que se procesan por análisis. El valor predeterminado es 2.

La configuración Intervalo de repetición y Tamaño de lote determina cuántos archivos recoge la carpeta inspeccionada en cada análisis. La carpeta inspeccionada utiliza un grupo de hilos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de análisis es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se pierden con frecuencia en la carpeta vigilada, reduzca el intervalo de análisis. Si los archivos se pierden con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

Si se pierde un gran volumen de archivos, aumente el tamaño del lote. Por ejemplo, si el servicio invocado por el extremo de la carpeta inspeccionada puede procesar 700 archivos por minuto y los usuarios pueden soltar archivos en la carpeta de entrada a la misma velocidad, al establecer el tamaño del lote en 350 y el intervalo de repetición en 30 segundos, ayudará al rendimiento de la carpeta inspeccionada sin incurrir en el coste de analizar la carpeta inspeccionada con demasiada frecuencia.

Cuando se sueltan los archivos en la carpeta vigilada, se enumeran los archivos en la entrada, lo que puede reducir el rendimiento si la exploración se realiza cada segundo. El aumento del intervalo de análisis puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y repita el intervalo según corresponda. Por ejemplo, si se sueltan 10 archivos cada segundo, intente establecer el intervalo de repetición en 1 segundo y el tamaño del lote en 10.

En una configuración de clúster, el tamaño de lote de un extremo de carpeta vigilada no se escala a varios nodos de clúster. Por ejemplo, si el tamaño del lote se establece en `2` para un clúster de dos nodos y se selecciona la opción Aceleración, los nodos procesan los archivos de forma colectiva en lotes de dos en lugar de que cada nodo procese dos archivos a la vez.

**Sobrescribir nombres de archivo duplicados:** Una cadena booleana que especifica si la carpeta vigilada sobrescribe los nombres de archivo de resultados duplicados y si se deben sobrescribir los documentos conservados con el mismo nombre.

**Conservar carpeta:** Valor predeterminado para la carpeta de conservación. Esta carpeta se utiliza para copiar los archivos de origen en si la entrada se procesa correctamente. Este valor puede ser una ruta vacía, relativa o absoluta con un patrón de archivo como se describe para la configuración Carpeta de resultados.

**Carpeta de error:** Nombre de la carpeta donde se copian los archivos de error. Este valor puede ser una ruta vacía, relativa o absoluta con un patrón de archivo como se describe para la configuración Carpeta de resultados.

**Carpeta de resultados:** El nombre predeterminado de la carpeta de resultados. Esta carpeta se utiliza para copiar los archivos de resultados en. Este valor puede ser una ruta vacía, relativa o absoluta con el siguiente patrón de archivo.

* %F = prefijo del nombre de archivo
* %E = extensión del nombre de archivo
* %Y = año (completo)
* %y = año (dos últimos dígitos)
* %M = mes
* %D = día del mes
* %d = día del año
* %H = hora (reloj de 24 horas)
* %h = hora (reloj de 12 horas)
* %m = minuto
* %s = segundo
* %l = milisegundo
* %R = número aleatorio (de 0 a 9)
* %P = ID del proceso o trabajo

Por ejemplo, si son las 20:00 del 17 de julio de 2009 y especifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la carpeta de resultados es `C:/Test/WF0/failure/2009/07/17/20`.

Si la ruta no es absoluta sino relativa, la carpeta se creará dentro de la carpeta vigilada. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Cuanto menor sea el tamaño de las carpetas de resultados, mejor será el rendimiento de la carpeta inspeccionada. Por ejemplo, si la carga estimada para la carpeta vigilada es de 1000 archivos cada hora, pruebe un patrón como `result/%Y%M%D%H` para que se cree una nueva subcarpeta cada hora. Si la carga es menor (por ejemplo, 1000 archivos por día), puede utilizar un patrón como `result/%Y%M%D`.

**Carpeta de fase:** El nombre predeterminado de la carpeta de fase dentro de la carpeta vigilada.

**Carpeta de entrada:** El nombre predeterminado de la carpeta de entrada dentro de la carpeta vigilada.

**Conservar si se produce error:** Si el valor es True, los archivos originales se conservarán en la carpeta de errores si se produce un error.

**Aceleración:** Cuando se selecciona esta opción, limita el número de trabajos de carpetas vigiladas que procesan los formularios AEM Forms en un momento dado. El valor Tamaño de lote determina el número máximo de trabajos (consulte Acerca de la restricción).

## Configuración del servicio Web {#web-service-service-settings}

El servicio Web (`WebService`) habilita procesos para invocar operaciones de servicio Web.

El servicio Web permite a los procesos invocar operaciones del servicio Web. Por ejemplo, una organización puede querer integrar un proceso para almacenar y recuperar información, como los detalles de contacto y cuenta, invocando los servicios web expuestos de un proveedor de servicios. El servicio Web Service invoca un servicio Web especificado y pasa los valores de cada uno de sus parámetros. A continuación, guarda los valores devueltos de la operación en una variable designada dentro de un proceso.

El servicio Web interactúa con los servicios Web mediante el envío y la recepción de mensajes de SOAP. El servicio también admite el envío de archivos adjuntos MIME, MTOM y SwaRef con mensajes SOAP mediante el protocolo WS-Attachment. Las interacciones del servicio Web son compatibles con los sistemas SAP y con los servicios Web .NET.

Las siguientes opciones de configuración están disponibles para el servicio Web.

**Almacén de claves:** Ruta de acceso completa del archivo de almacén de claves que contiene la clave privada que se va a utilizar para la autenticación. El servidor de Forms debe poder acceder al archivo.

**Contraseña de almacén de claves:** Contraseña del archivo de almacén de claves.

**Tipo de almacén de claves:** Tipo de almacén de claves. No proporcione ningún valor para utilizar el tipo de almacén de claves predeterminado configurado para la JVM que ejecuta el servidor de Forms. De lo contrario, proporcione uno de los siguientes valores:

* jks
* pkcs12
* cms
* jceks

**Almacén de confianza:** Ruta de acceso completa del archivo del almacén de confianza que contiene la clave pública del servidor de servicio web.

**Contraseña del almacén de confianza:** Contraseña del archivo truststore.

**Tipo de almacén de confianza:** Tipo de almacén de confianza. No proporcione ningún valor para utilizar el tipo de almacén de claves predeterminado configurado para la JVM que ejecuta el servidor de Forms. De lo contrario, proporcione uno de los siguientes valores:

* jks
* pkcs12
* cms
* jceks

## Configuración del servicio de transformación XSLT {#xslt-transformation-service-settings}

El servicio de transformación XSLT (`XSLTService`) permite a los procesos aplicar transformaciones XSLT (Extensible Stylesheet Language Transformations) en documentos XML.

La siguiente configuración está disponible para el servicio Transformación XSLT.

**Nombre de fábrica:** El nombre completo de la clase Java que se va a utilizar para realizar transformaciones XSLT. Si no se especifica ningún valor, se utiliza el generador predeterminado configurado en la máquina virtual Java que ejecuta el servidor de Forms.

## Modificación de la configuración de seguridad de un servicio {#modifying-security-settings-for-a-service}

El servidor de Forms le permite configurar las opciones de seguridad de cada servicio, lo que le permite configurar un control de acceso detallado en un nivel de servicio a servicio.

Se instalan los perfiles de seguridad predeterminados, que se pueden configurar para satisfacer las necesidades del sistema. Cada perfil de seguridad tiene un dominio asociado y se crea en el nivel de usuario o de grupo.

### Modificar la configuración de seguridad de un servicio {#modify-security-settings-for-a-service}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la pestaña Seguridad.
1. En la lista Requerir que los llamadores se autentiquen, seleccione Sí o No para especificar si el servicio se puede invocar con o sin credenciales.

   Si selecciona Sí, el llamador del servicio debe estar autenticado y el principal de usuario de ese llamador debe estar autorizado para invocar el servicio; de lo contrario, se rechazará el intento de invocación.

   Si selecciona No, la persona que llama al servicio puede estar autenticada o no. La invocación del servicio siempre se realizará correctamente porque no hay ninguna comprobación de autorización.

1. Para los servicios que contienen una o más operaciones marcadas para acceso anónimo, seleccione o anule la selección de Acceso anónimo permitido. Cuando el acceso anónimo está habilitado, cualquier usuario del sistema puede invocar operaciones en el servicio. Si el acceso anónimo está deshabilitado, los usuarios deben tener permiso para llamar al servicio e invocar operaciones. A los usuarios se les conceden estos permisos directamente o como parte de un grupo que los tiene.
1. En algunos servicios, la cuenta de usuario que ejecuta la operación afecta a los resultados. Por ejemplo, en Content Services (obsoleto), el usuario que almacena contenido pasa a ser el propietario del contenido, lo que afecta a quién puede acceder posteriormente al contenido. Si está utilizando un proceso para almacenar contenido, piense en qué usuario se utiliza para ejecutar el servicio de Administración de documentos, ya que ese usuario será el propietario del contenido almacenado.

   Para especificar la identidad en tiempo de ejecución utilizada por un servicio para ejecutar operaciones, seleccione Especificar Ejecutar como, seleccione una opción de la lista asociada y, a continuación, haga clic en Guardar. Elija entre las siguientes opciones:

   **Invocador:** Usa la misma identidad que el usuario que invocó el servicio.

   **Sistema:** utiliza al usuario del sistema para ejecutar el servicio con privilegios completos.

   **Usuario designado:** Permite ejecutar el servicio como un usuario específico. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar al usuario.

   Si no selecciona Especificar ejecutar como, se utilizará el comportamiento predeterminado.

   >[!NOTE]
   >
   >Los servicios de procesamiento y envío que se utilizan con las variables xfaForm, Document Form y Form se ejecutan siempre con la cuenta de usuario del sistema.

1. Haga clic en Agregar entidad principal para especificar los permisos que tienen los usuarios y grupos para este servicio.
1. La pantalla Seleccionar principal muestra los usuarios y grupos configurados en Administración de usuarios. Si el usuario o grupo que desea no aparece, utilice la función de búsqueda para encontrarlo. Haga clic en el nombre de un usuario o grupo.
1. En la pantalla Agregar permisos, seleccione los permisos que desea asignar al usuario o grupo para este servicio:

   * **INVOKE_PERM:** Para invocar todas las operaciones del servicio
   * **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio
   * **SUPERVISOR_PERM:** Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso
   * **START_STOP_PERM:** Para iniciar y detener un servicio
   * **ADD_REMOVE_ENDPOINTS_PERM:** Para agregar, quitar y modificar extremos de un servicio
   * **CREATE_VERSION_PERM:** Para crear una versión del servicio
   * **DELETE_VERSION_PERM:** Para eliminar una versión del servicio
   * **MODIFY_VERSION_PERM:** Para modificar una versión del servicio
   * **READ_PERM:** Para ver el servicio
   * **PROCESS_OWNER_PERM:** para su uso en una versión futura de formularios AEM. No utilice este permiso.
   * **SERVICE_MANAGER_PERM:** para su uso en una versión futura de formularios AEM. No utilice este permiso.
   * **SERVICE_AGENT_PERM:** para su uso en una versión futura de formularios AEM Forms. No utilice este permiso.

1. Haga clic en Agregar.

### Quitar el principal de un perfil de seguridad {#remove-the-principal-from-a-security-profile}

1. En la página Administración de servicios, seleccione el servicio que desea configurar.
1. Haga clic en la ficha **Seguridad**, seleccione el perfil de seguridad que desea quitar y haga clic en **Quitar**.

## Configuración de la agrupación para un servicio {#configuring-pooling-for-a-service}

Cada servicio puede aprovechar las capacidades de agrupación para administrar las solicitudes de invocación entrantes. El uso de un grupo de servicios garantiza que las instancias de servicio se invoquen mediante un único subproceso a la vez y se reutilicen en las solicitudes de invocación, lo que puede mejorar el rendimiento. También puede utilizar la agrupación para especificar la opción Máximo de instancias de servicio asincrónicas, que permite a los servicios limitar el número de solicitudes gestionadas en paralelo.

### Activar agrupación {#enable-pooling}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la pestaña Pooling.
1. En la lista Estrategia de procesamiento de solicitudes, seleccione Instancias agrupadas para todas las solicitudes.
1. En el cuadro Tamaño del grupo de instancias de servicio inicial, introduzca el tamaño inicial del grupo. Cuando se implementa el servicio, este número se utiliza para determinar el número de instancias de implementación del servicio que se crean y asignan al grupo libre, a la espera de solicitudes de invocación. Esto permite que el contenedor de servicio responda inmediatamente a las solicitudes de invocación sin tener que inicializar primero una instancia de servicio.
1. En el cuadro Tamaño máximo del grupo de instancias de servicio, introduzca el número máximo de instancias en el grupo para un servicio determinado. Esta configuración controla el número de subprocesos que pueden ejecutar un servicio determinado en un momento determinado. El valor predeterminado es 0, lo que da como resultado un tamaño de grupo ilimitado.
1. En el cuadro Máximo de instancias de servicio asincrónico, escriba el número máximo de instancias del grupo que se pueden usar para atender solicitudes asincrónicas en un momento dado. Esta configuración permite al servicio limitar el número de solicitudes que puede administrar en paralelo.
1. En el cuadro Tiempo de espera de invocación, escriba el número de milisegundos que hay que esperar para que un servicio esté disponible para una solicitud de invocación. Si no especifica un valor para esta configuración, el valor predeterminado es 0, lo que no provoca que se produzca ningún tiempo de espera.
1. Haga clic en Guardar.

### Quitar agrupación {#remove-pooling}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la pestaña Pooling.
1. En la lista Estrategia de procesamiento de solicitudes, seleccione Nueva instancia para cada solicitud o Instancia única para todas las solicitudes.

   **Instancia única para todas las solicitudes:** Se crea una instancia de servicio y se almacena en caché cuando la primera solicitud llega al contenedor. Cada solicitud posterior a esa solicitud utiliza la misma instancia de servicio para administrar la solicitud.

   **Nueva instancia para cada solicitud:** Se crea una nueva instancia de servicio para cada invocación recibida.

1. Haga clic en Guardar.
