---
title: Descripción general de AEM Document Services
description: AEM Document Services es un conjunto de servicios OSGi para crear, ensamblar y proteger documentos PDF.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Reader Extensions, Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 100%

---

# Descripción general de AEM Document Services{#overview-of-aem-document-services}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=es) |
| AEM 6.5 | Este artículo |


AEM Document Services es un conjunto de servicios OSGi para crear, ensamblar y proteger documentos PDF. Document Services contiene los siguientes servicios:

## Servicio de salida {#output-service}

El servicio Output permite crear documentos en diferentes formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Lenguaje de control de impresora (PCL). La siguiente lista especifica los formatos de impresora de etiquetas:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Un documento se puede enviar a una impresora de red, a una impresora local o a un archivo del sistema de archivos. El servicio Output combina los datos de formulario XML con un diseño de formulario para generar un documento. El servicio Output puede generar un documento sin combinar los datos de formulario XML en el documento. Sin embargo, el flujo de trabajo principal consiste en combinar datos en el documento.

>[!NOTE]
>
>Normalmente, los diseños de formulario se crean con Designer. Para obtener información sobre la creación de diseños de formulario para el servicio Output, consulte la Ayuda de Designer.

Cuando se utiliza el servicio Output para combinar datos XML con un diseño de formulario, el resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en los campos. En cambio, puede utilizar el servicio Forms para crear un formulario PDF interactivo que permita a los usuarios introducir datos en sus campos.

Hay disponibles para su uso las cuatro operaciones del servicio Output que aparecen a continuación:

* **generatePDFOuput**: combina un diseño de formulario con datos para generar un documento PDF.
* **generatePrintedOutput**: combina un diseño de formulario con datos de formulario para generar un documento que se enviará a una impresora de red láser o de etiquetas.

* **generatePDFOutputBatch**: combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de archivos PDF. También existe la opción de generar un único PDF combinando los restantes.
* **generatePrintedOutputBatch**: combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de documentos de impresión (PS, PCL, ZPL, DPL, IPL y TPCL). También hay una opción para generar un solo documento de impresión.

## Servicio Assembler {#assembler-service}

El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF. Cada trabajo enviado al servicio Assembler incluye un documento XML de descripción de documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). El documento DDX proporciona instrucciones sobre cómo utilizar los documentos de origen para producir un conjunto de documentos resultantes.

Además de las capacidades mencionadas anteriormente, el servicio Assembler:

* Convierte documentos PDF en estándar PDF/A.
* Transforma formularios PDF, formularios XML (creados en Designer) y formularios PDF (creados en Acrobat) en PDF/A-1b, PDF/A-2b y PDFA/A-3b.
* Convierte documentos PDF firmados o no firmados (se requiere Firmas digitales).
* Valida la conformidad de un archivo PDF/A y lo convierte si es necesario.

### Acerca de DDX {#about-ddx}

Al utilizar el servicio Assembler, use el lenguaje basado en XML denominado XML de descripción de documento (DDX) para describir la salida que desea. DDX es un lenguaje de marcado declarativo cuyos elementos representan componentes básicos de documentos. Estos componentes básicos incluyen documentos PDF, documentos XDP, fragmentos de formulario XDP y otros elementos como comentarios, marcadores y texto con estilo.

El documento DDX puede especificar documentos resultantes con estas características:

* Un documento PDF ensamblado a partir de varios documentos PDF
* Varios documentos PDF divididos a partir de un solo documento PDF
* Un portafolio PDF con una interfaz de usuario independiente y varios documentos PDF y no PDF
* Un documento XDP ensamblado a partir de varios documentos XDP
* Un documento XDP que contiene fragmentos XML insertados dinámicamente en un documento XDP
* Un documento PDF que empaqueta un documento XDP
* Archivos XML que contienen información sobre las características de un documento PDF. Se incluye información sobre características como texto, comentarios, datos de formulario, archivos adjuntos, archivos utilizados en portafolios PDF, marcadores y propiedades PDF. Entre las propiedades PDF se incluyen las propiedades de formulario, la rotación de páginas y el autor del documento.

Puede utilizar DDX para aumentar documentos PDF como parte del ensamblado o desensamblado del documento. Puede especificar cualquier combinación de los siguientes efectos:

* Agregar o quitar marcas de agua o fondos en las páginas seleccionadas.
* Agregar o quitar encabezados y pies de página en las páginas seleccionadas.
* Eliminar la estructura y las capacidades de navegación de un portafolio o paquete PDF. El resultado es un solo archivo PDF.
* Cambiar la numeración de las etiquetas de página. Las etiquetas de página suelen utilizarse en la numeración de páginas.
* Importar metadatos de otro documento de origen.
* Agregar o quitar archivos adjuntos, marcadores, vínculos, comentarios y JavaScript.
* Definir las características de la vista inicial y optimizar la visualización en la web.
* Establecer permisos para PDF cifrados.
* Rotar páginas o rotar y desplazar contenido en páginas.
* Cambiar el tamaño de las páginas seleccionadas.
* Combinar datos con un PDF basado en XFA.

Puede utilizar un mapa de entrada simple para especificar las ubicaciones de los documentos de origen y los documentos resultantes. También puede utilizar los siguientes tipos de URL de datos externos:

* Archivo
* FTP
* HTTP/HTTPS

## Servicio Doc Assurance {#doc-assurance-service}

El servicio Doc Assurance le permite cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y añadir firmas digitales a sus documentos. Los usuarios pueden interactuar fácilmente con los formularios y los documentos PDF mientras su organización mejora la seguridad, el archivo y el cumplimiento normativo.

El servicio Doc Assurance contiene tres servicios: Signature, Encryption y Extensiones de Reader.

### Servicio Signature {#signature-service}

El servicio Signature le permite trabajar con firmas y documentos digitales en el servidor de AEM. Por ejemplo, el servicio Signature se suele utilizar en las siguientes situaciones:

* El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra con Acrobat o Adobe Reader.
* El servidor de AEM valida una firma que se ha agregado a un formulario mediante Acrobat o Adobe Reader.
* El servidor de AEM firma un formulario en nombre de un notario público.

El servicio Signature accede a los certificados y credenciales almacenados en el almacén de confianza.

### Servicio Encryption {#encryption-service}

El servicio Encryption permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Puede cifrar todo el documento PDF (incluido el contenido, los metadatos y los archivos adjuntos), todo salvo los metadatos, o solo los archivos adjuntos. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña de apertura para poder visualizar el documento en Adobe Reader o Acrobat. Si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con una clave privada (certificado). La clave privada utilizada para descifrar el documento del PDF debe corresponder a la clave pública utilizada para cifrarlo.

### Servicio Extensiones de Reader {#reader-extension-service}

El servicio Extensiones de Reader permite a su organización compartir fácilmente documentos PDF interactivos ampliando la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio Extensiones de Reader es compatible con Adobe Reader 7.0 o versiones posteriores. El servicio agrega derechos de uso a un documento PDF. Esta acción activa funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Los usuarios de terceros no requieren software ni complementos adicionales para trabajar con los documentos con derechos activados.

Cuando se agregan los derechos de uso correspondientes a los documentos PDF, los destinatarios pueden realizar las siguientes actividades desde Adobe Reader:

* completar documentos y formularios PDF en línea o sin conexión, lo que permite a los destinatarios guardar copias de forma local para sus registros y mantener intacta la información agregada;
* guardar los documentos PDF en un disco duro local para conservar el documento original y los comentarios, datos o archivos adjuntos adicionales;
* adjuntar archivos y clips de medios en documentos PDF;
* firmar, certificar y autenticar documentos PDF mediante la aplicación de firmas digitales con tecnologías de infraestructura de clave pública (PKI) conformes con los estándares del sector;
* enviar documentos PDF completados o anotados electrónicamente;
* utilizar documentos y formularios PDF como un front-end de desarrollo intuitivo para bases de datos y servicios web internos;
* compartir documentos PDF con terceros para que los revisores puedan agregar comentarios mediante herramientas de marcado intuitivas. Entre estas herramientas se incluyen las notas adhesivas electrónicas, los sellos, los resaltados y el tachado de texto. Estas funciones también están disponibles en Acrobat;
* admitir la descodificación de formularios con códigos de barras.

Estas funciones de usuario especiales se activan automáticamente al abrir un documento PDF con los derechos activados en Adobe Reader. Cuando el usuario ha terminado de trabajar con un documento con derechos activados, esas funciones vuelven a desactivarse en Adobe Reader. Permanecen desactivados hasta que el usuario recibe otro documento PDF con los derechos activados.

El servicio DocAssurance no está disponible para su uso de forma predeterminada. Para configurar el servicio DocAssurance, consulte [Instalación y configuración de Document Services](../../forms/using/install-configure-document-services.md).

## Servicio Enviar a impresora {#send-to-printer-service}

El servicio Enviar a impresora proporciona una API para enviar documentos a una impresora especificada para su impresión.
