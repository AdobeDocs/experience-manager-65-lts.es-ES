---
title: Convertir archivos mediante el generador de PDF
description: El servicio PDF Generator convierte los formatos de archivo nativos a PDF. También convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1d2adc53-498f-43f5-b664-0b9dd864b9a1
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 3%

---

# Convertir archivos mediante el generador de PDF{#converting-files-using-pdf-generator}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede utilizar las páginas web de PDF Generator para convertir archivos.

## Creación de un archivo de PDF {#create-a-pdf-file}

1. En la consola de administración, haga clic en Servicios > PDF Generator > Crear PDF.
1. Haga clic en Examinar para buscar y seleccionar el archivo.

   >[!NOTE]
   >
   >PDF Generator puede detectar automáticamente el tipo de archivo de los archivos .doc, .xls, .ppt y .rtf, incluso cuando falta la extensión de archivo en el nombre del archivo. Esta función no funciona con archivos .docx, .xlsx y .pptx.

1. En Configuración, seleccione Usar configuración personalizada o Cargar archivo de configuración.

   * Si utiliza la configuración personalizada, seleccione una configuración de Adobe PDF, de seguridad y de tipo de archivo, y especifique un tiempo de espera.

     La configuración de Adobe PDF solo se aplica a las conversiones de PS a PDF, de EPS a PDF, de PRN a PDF, de imagen a PDF con OCR activado y de nativo a PDF. La configuración de tiempo de espera especifica el tiempo máximo que tarda la conversión en completarse. El valor predeterminado es 270 segundos. Esta configuración no se utiliza durante las conversiones de imagen a PDF y de OpenOffice a PDF.

   * Si está cargando un archivo de configuración, escriba su ruta y nombre en el cuadro o haga clic en Examinar para buscar y seleccionar el archivo.

1. (Opcional) En Archivo de metadatos de XMP, escriba la ruta y el nombre del archivo de XMP o haga clic en Examinar para buscar y seleccionar el archivo. Se puede utilizar un archivo XMP para incluir información de metadatos estándar. (Consulte [Acerca de los archivos de XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Haga clic en Crear. Cuando se crea el archivo, aparece un vínculo con él. Si se produce un error durante la conversión, aparece una advertencia. Si está creando un archivo Postscript, la advertencia también contendrá un vínculo al archivo de registro.
1. Haga clic en el vínculo del archivo PDF. El archivo se abre en Acrobat.

### Acerca de los archivos XMP {#about-xmp-files}

Los documentos de PDF que PDF Generator crea en Acrobat 5.0 o posterior contienen metadatos de documento en formato XML. *Metadatos* incluye información sobre el documento y su contenido, como el nombre del autor, palabras clave e información de copyright que las utilidades de búsqueda pueden utilizar.

Los metadatos del documento contienen, entre otras cosas, información que también aparece en la ficha Descripción del cuadro de diálogo Propiedades del documento de Acrobat. Los cambios realizados en la ficha Descripción se reflejan en los metadatos del documento. Los metadatos del documento se pueden ampliar y modificar mediante productos de terceros.

Adobe Extensible Metadata Platform (XMP) proporciona a las aplicaciones de Adobe un marco XML común que estandariza la creación, el procesamiento y el intercambio de metadatos de documentos en los flujos de trabajo de publicación. Puede guardar e importar el código fuente XML de metadatos del documento en formato XMP, lo que facilita el uso compartido de metadatos entre varios documentos. Para obtener más información sobre los archivos de XMP, consulte [Extensible Metadata Platform (XMP)](https://www.adobe.com/products/xmp/) y [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html).

Puede crear archivos de XMP en Acrobat.

## Conversión de un archivo HTML o ZIP a PDF {#convert-an-html-file-or-zip-file-to-pdf}

Puede utilizar PDF Generator para convertir los siguientes tipos de archivos a Adobe PDF:

* Archivos HTML, que se pueden convertir cargando un archivo HTML o especificando la dirección URL de una página web o sitio web.
* Archivos archivados (ZIP), que pueden contener archivos de HTML, archivos de imagen o ambos.

Si el archivo ZIP contiene más de un archivo HTML en el nivel inferior de su jerarquía de carpetas, el archivo ZIP también debe contener un archivo index.htm o index.html.

>[!NOTE]
>
>* La función de HTML a PDF requiere ciertas fuentes en el directorio de fuentes del sistema. En los sistemas Linux, Solaris y AIX, el directorio de fuentes del sistema debe contener la fuente Courier. En sistemas Windows, el directorio de fuentes del sistema debe contener Times New Roman.
>
>* (Solo sistema basado en UNIX) Una de las siguientes fuentes japonesas debe estar disponible en el servidor de AEM Forms para convertir una página web con fuente japonesa en un documento de PDF.
>
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* Para cargar un archivo desde el sistema de archivos local, utilice la opción Upload File de la página HTML to PDF.

1. En la consola de administración, haga clic en Servicios > PDF Generator > HTML a PDF.
1. Especifique el archivo que desea convertir mediante una de las siguientes tareas:

   * En Cargar archivo, escriba la ruta y el nombre del archivo HTML o ZIP, o haga clic en Examinar para buscarlo y seleccionarlo.
   * En el cuadro Especificar URL, escriba la dirección URL de la página o sitio web que desea convertir.

   >[!NOTE]
   >
   >El archivo que está convirtiendo debe tener la extensión de nombre de archivo .html, .htm o .zip.

1. Especifique los ajustes de configuración:

   * Para usar la configuración personalizada, seleccione Usar configuración personalizada, especifique la configuración de seguridad y tipo de archivo, y especifique un valor de tiempo de espera. El valor predeterminado es 270 segundos.

   >[!NOTE]
   >
   >Si configuró el servicio Generate PDF para utilizar Acrobat WebCapture, la configuración de tipo de archivo que seleccione en esta página no afectará a la configuración de PDF producida. En su lugar, realice los cambios correspondientes en la versión de Acrobat instalada en el servidor.

   * Para utilizar un archivo de configuración existente, seleccione Cargar archivo de configuración y haga clic en Examinar para ir a la ubicación del archivo.

1. Para cargar un archivo de XMP, haga clic en Examinar y vaya a la ubicación del archivo. Se puede utilizar un archivo XMP para incluir información de metadatos estándar. (Consulte [Acerca de los archivos de XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Haga clic en Crear. Cuando se crea el archivo, aparece un vínculo al archivo PDF.
1. Haga clic en el vínculo para ver el documento de PDF en Acrobat.

## Exportar un archivo de PDF a otro formato de archivo (sólo Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

Puede exportar archivos de PDF a varios formatos, tal como se describe en el capítulo Generate PDF Service de [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

1. En la consola de administración, haga clic en Servicios > PDF Generator > Export PDF.
1. Haga clic en Examinar para buscar el archivo de PDF que desea exportar.
1. En la lista Export PDF file to, seleccione el formato al que desea exportar el archivo PDF.
1. En el cuadro Especificar un tiempo de espera, escriba el tiempo de espera antes de que se agote el tiempo de espera de la aplicación. El valor predeterminado es 270 segundos.

   El Tiempo de conversión que se muestra cuando se convierte el archivo puede ser mayor que el valor especificado aquí. El Tiempo de conversión incluye el tiempo empleado esperando el subproceso o proceso, el tiempo empleado para convertir el archivo y el tiempo empleado por el convertidor de reserva (si corresponde). hora. Especificar un valor de tiempo de espera es solo el tiempo necesario para convertir el archivo.

1. (Opcional) En la opción **Especificar perfil de comprobaciones personalizado**, haga clic en Examinar y seleccione un [perfil de comprobaciones personalizado](https://helpx.adobe.com/es/acrobat/using/preflight-profiles-acrobat-pro.html). Los perfiles de comprobación preliminar solo se utilizan al convertir documentos al formato de archivo de PDF (PDF/A).
1. Haga clic en Exportar. Cuando finaliza la conversión, aparece un vínculo al archivo exportado.
1. Haga clic en el vínculo para ver el archivo convertido.

## Optimización de un PDF (solo Windows) {#optimize-a-pdf}

PDF Generator admite la reducción del tamaño de los archivos de PDF.

>[!NOTE]
>
>Al optimizar un documento firmado digitalmente, se eliminan y se invalidan las firmas digitales.

1. En la consola de administración, haga clic en Servicios > PDF Generator > Optimizar PDF.
1. Haga clic en Examinar para buscar el archivo de PDF que desea optimizar.
1. Especifique los ajustes de configuración:

   * Para usar la configuración personalizada, seleccione Usar configuración personalizada, especifique la configuración del tipo de archivo y especifique un valor de tiempo de espera. El valor predeterminado es 270 segundos.
   * Para utilizar un archivo de configuración existente, seleccione Cargar archivo de configuración y haga clic en Examinar para ir a la ubicación del archivo.

1. Haga clic en Crear.
