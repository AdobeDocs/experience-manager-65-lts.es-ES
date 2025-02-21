---
title: Usar el servicio Assembler
description: El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF.
feature: Document Services
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 94%

---

# Usar el servicio Assembler{#using-assembler-service}

El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF. Cada trabajo enviado al servicio Assembler incluye un documento XML de descripción de documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). Para obtener más información sobre el servicio Assembler, consulte [Descripción general del servicio Assembler](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

Puede utilizar el servicio Assembler para las siguientes operaciones:

## Montar los documentos PDF {#assemble-pdf-documents}

Puede utilizar el servicio Assembler para juntar dos o más documentos PDF en un único documento PDF o portfolio PDF. También puede aplicar características al documento PDF que ayuden a la navegación o que mejoren la seguridad. A continuación se indican algunas formas de montar documentos PDF:

### Montar un documento PDF sencillo {#assemble-a-simple-pdf-document}

La siguiente ilustración muestra tres documentos que se combinan en uno solo resultante.

![Combinar un documento PDF simple desde varios documentos PDF](assets/as_document_assembly.png)

Combinar un documento PDF simple desde varios documentos PDF

El siguiente ejemplo es un documento DDX simple que se utiliza para combinar el documento. Especifica los nombres de los documentos de origen utilizados para producir el documento resultante y el nombre del documento resultante:

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

Al combinar los documentos, se produce un documento resultante que contiene el siguiente contenido y\
características:

* Todo o parte de cada documento de origen
* Todo o parte de los marcadores de cada documento de origen, normalizados para el documento resultante
* Otras características adoptadas a partir del documento base (Doc1), incluidos metadatos, etiquetas de página y tamaño de página
* Opcionalmente, el documento resultante incluye una tabla de contenido creada a partir de los marcadores de los documentos de origen

### Crear un portfolio PDF {#create-a-pdf-portfolio}

El servicio Assembler puede crear portfolios PDF que contengan una colección de documentos y una interfaz de usuario independientes. La interfaz se denomina Diseño del portfolio PDF o navegador del portfolio PDF (navegador). Los portfolios PDF amplían la capacidad de los paquetes PDF al agregar un explorador, carpetas y páginas de bienvenida. La interfaz puede mejorar la experiencia del usuario al aprovechar la cadena de texto localizada, los esquemas de color personalizados y los recursos gráficos. El portfolio PDF también puede incluir carpetas para organizar sus archivos.

Cuando el servicio Assembler interpreta el siguiente documento DDX, combina un portfolio PDF que incluye un navegador portfolio PDF y un paquete de dos archivos. El servicio obtiene el navegador de la ubicación especificada por la fuente myNavigator. Cambia el esquema de colores predeterminado del navegador al esquema de colores pinkScheme.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### Combinar documentos cifrados {#assemble-encrypted-documents}

Al combinar un documento, también puede cifrar el documento PDF con una contraseña. Una vez que un documento PDF esté cifrado con una contraseña, los usuarios deberán especificar la contraseña para ver el documento PDF en Adobe Reader o Acrobat. Para cifrar un documento PDF con una contraseña, el documento DDX debe contener valores de elementos de cifrado necesarios para cifrar un documento PDF.

El servicio de cifrado no tiene que formar parte de la instalación del LiveCycle para cifrar un documento PDF con una contraseña.

Si uno o más documentos de entrada están cifrados, proporcione una contraseña para abrir el documento como parte del DDX.

### Combinar documentos mediante la numeración Bates {#assemble-documents-using-bates-numbering}

Al combinar un documento, puede utilizar la numeración Bates para aplicar un identificador de página único a cada página. Al utilizar la numeración Bates, a cada página del documento (o conjunto de documentos) se le asigna un número que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información de listas de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + valor numérico + sufijo se denomina patrón de fechas.

La siguiente ilustración muestra un documento de PDF que contiene un identificador único en el encabezado del documento.

![Documento de PDF que contiene un identificador único en el encabezado del documento](do-not-localize/as_batesnumber.png)

Documento de PDF que contiene un identificador único en el encabezado del documento

### Acoplar y combinar documentos {#flatten-and-assemble-documents}

Puede utilizar el servicio Assembler para transformar un documento PDF interactivo (por ejemplo, un formulario) en un documento de PDF no interactivo. Un documento interactivo de PDF permite a los usuarios introducir o modificar datos en los campos del documento de PDF. El proceso de transformar un documento PDF interactivo en uno no interactivo se denomina aplanamiento. Cuando se aplana un documento PDF, los campos de formulario conservan su apariencia gráfica, pero ya no son interactivos. Una razón para acoplar un documento PDF es garantizar que no se puedan modificar los datos. Además, los scripts asociados a los campos ya no funcionan.

Cuando se crea un documento de PDF que se monta a partir de documentos PDF interactivos, el servicio Assembler aplana dichos formularios antes de combinarlos en el documento resultante.

>[!NOTE]
>
>El servicio Assembler utiliza el servicio Output para aplanar formularios XFA dinámicos. Si el servicio Assembler procesa un DDX que requiere que aplane un formulario dinámico XFA y el servicio Output no está disponible, se generará una excepción. El servicio Assembler puede aplanar un formulario Acrobat o un formulario XFA estático sin utilizar el servicio Output.

## Agrupar documentos XDP {#assemble-xdp-documents}

Puede utilizar el servicio Assembler para aplanar varios documentos XDP en uno solo o en un documento PDF. Para los archivos XDP de origen que incluyen puntos de inserción, puede especificar los fragmentos que desea insertar.

A continuación se indican algunas formas de montar documentos XDP:

### Montar un documento XDP sencillo {#assemble-a-simple-xdp-document}

La siguiente ilustración muestra tres documentos XDP de origen que se combinan en un único documento XDP resultante. El documento XDP resultante contiene los tres documentos XDP de origen, incluidos sus datos asociados. El documento resultante obtiene atributos básicos del documento base, que es el primer documento XDP de origen.

![Combinar un documento XDP simple desde varios documentos XDP](assets/as_assembler_xdpassembly.png)

Combinar un documento XDP simple desde varios documentos XDP

Este es un documento DDX que produce el resultado ilustrado anteriormente.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### Resolver referencias durante la combinación {#resolving-references-during-assembly}

Normalmente, los documentos XDP pueden contener imágenes a las que se hace referencia mediante referencias absolutas o relativas. El servicio Assembler, de forma predeterminada, conserva las referencias a las imágenes en el documento XDP resultante.

Puede especificar cómo administra el servicio Assembler las imágenes a las que se hace referencia en los documentos XDP de origen mediante referencias absolutas o relativas en los archivos XDP al combinarlos. Puede elegir que todas las imágenes estén incrustadas en el resultado, de modo que no contenga referencias relativas o absolutas. Puede definirlo al establecer el valor de la etiqueta resolveAssets, que puede utilizar cualquiera de las siguientes opciones. De forma predeterminada, no se resuelve ninguna referencia en el documento de resultados.

<table>
 <tbody> 
  <tr> 
   <th>Valor</th> 
   <th>Descripción</th> 
  </tr> 
  <tr> 
   <td>ninguno</td> 
   <td>No resuelve ninguna referencia.</td> 
  </tr> 
  <tr> 
   <td>todo</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia en el documento XDP de origen.</td> 
  </tr> 
  <tr> 
   <td>relativo</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias relativas en el XDP de origen<br /> documento.</td> 
  </tr> 
  <tr> 
   <td>absoluto</td> 
   <td>Incrusta todas las imágenes a las que se hace referencia mediante referencias absolutas en el documento XDP de origen<br />.</td> 
  </tr> 
 </tbody> 
</table>

Puede especificar el valor del atributo resolveAssets en la etiqueta de origen XDP o en la etiqueta de resultado XDP principal. Si el atributo se especifica en la etiqueta de resultado XDP, todos los elementos de origen XDP que sean secundarios del resultado XDP lo heredarán. Sin embargo, si se especifica explícitamente el atributo para un elemento de origen, solo se anulará la configuración del elemento de resultado para ese documento de origen.

#### Resolver todas las referencias de origen en un documento XDP {#resolve-all-source-references-in-an-xdp-document}

Para resolver todas las referencias en los documentos XDP de origen, especifique el atributo resolveAssets para el\
documento resultante para todos, como en el siguiente ejemplo:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

También puede especificar el atributo para todos los documentos XDP de origen de forma independiente para obtener el mismo\
resultado.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### Resolver referencias de origen seleccionadas en un documento XDP {#resolve-selected-source-references-in-an-xdp-document}

Puede especificar selectivamente las referencias de origen que desea resolver al especificar el atributo resolveAssets para ellas. Los atributos de los documentos de origen individuales anulan la configuración del documento XDP resultante. En este ejemplo, los fragmentos incluidos también se resuelven.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### Resolver referencias en el repositorio de CRX {#resolve-references-on-crx-repository}

Puede especificar selectivamente la referencia de origen que desea resolver indicando la ruta CRX del
referencia de fragmento en el origen XDP. En el siguiente ejemplo, los fragmentos incluidos también se
resuelto.

```xml
<DDX xmlns="http://ns.adobe.com/DDX/1.0/"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://ns.adobe.com/DDX/1.0/ coldfusion_ddx.xsd">
<XDP result="stitched.xdp">
<XDP source="crx:///content/dam/formsanddocuments/test-xdp/sample.xdp" />
</XDP>
</DDX>
```

#### Resolución selectiva de referencias absolutas o relativas {#selectively-resolve-absolute-or-relative-references}

Puede resolver selectivamente referencias absolutas o relativas en todos o algunos de los documentos de origen, como se muestra en el siguiente ejemplo:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### Insertar dinámicamente fragmentos de formulario en un formulario XFA {#dynamically-insert-form-fragments-into-an-xfa-form}

Puede utilizar el servicio Assembler para crear un formulario XFA creado a partir de otro formulario XFA en el que se insertan fragmentos. Con esta función, puede utilizar fragmentos para crear varios formularios.

La compatibilidad con la inserción dinámica de fragmentos de formulario admite el control de un solo origen. Se mantiene una única fuente de componentes utilizados con frecuencia. Por ejemplo, puede crear un fragmento para el banner de la empresa. Si el banner cambia, solo tiene que modificar el fragmento. Los demás formularios que incluyen el fragmento no cambiarán.

Los diseñadores de formularios utilizan LiveCycle Designer para crear fragmentos de formulario. Estos fragmentos son subformularios con un nombre único dentro de un formulario XFA. Los diseñadores de formularios también utilizan Designer para crear formularios XFA con nombres únicos. Usted (el programador) escribe documentos DDX que especifican cómo se insertan los fragmentos en el formulario XFA.

La siguiente ilustración muestra dos formularios XML (plantillas XFA). El formulario de la izquierda contiene un punto de inserción denominado myInsertionPoint. El formulario de la derecha contiene un fragmento llamado myFragment.

![Insertar fragmentos de formulario en un formulario XFA](assets/as_assembler_fragment_assy_assembled.png)

Insertar fragmentos de formulario en un formulario XFA

Cuando el servicio Assembler interpreta el siguiente documento DDX, crea un formulario XML que contiene otro formulario XML. El subformulario myFragment del documento myFragmentSource se inserta en myInsertionPoint en el documento myFormSource.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### Empaquetar un documento XDP como PDF {#package-an-xdp-document-as-pdf}

Puede utilizar el servicio Assembler para empaquetar un documento XDP como documento PDF, como se muestra en este documento DDX.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## Desmontar los documentos PDF {#disassemble-pdf-documents}

Puede utilizar el servicio Assembler para desmontar un documento PDF. El servicio puede extraer páginas del documento de origen o dividir un documento fuente en base a marcadores. Normalmente, esta tarea resulta útil si el documento PDF se creó originalmente a partir de numerosos documentos individuales, como una colección de declaraciones.

### Extraer páginas de un documento fuente {#extract-pages-from-a-source-document}

En la siguiente ilustración, las páginas 1 a 3 se extraen del documento de origen y se colocan en un nuevo documento resultante.

![Extraer páginas específicas de un documento de origen](assets/as_intro_page_extraction.png)

Extraer páginas específicas de un documento de origen

El siguiente ejemplo es un documento DDX utilizado para desmontar el documento.

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### Dividir un documento fuente basado en marcadores {#divide-a-source-document-based-on-bookmarks}

En la siguiente ilustración, el DocA se divide en varios documentos resultantes. El primer marcador de nivel 1 de una página identifica el inicio de un documento resultante nuevo.

![Dividir un documento de origen basado en marcadores en varios documentos](assets/as_intro_pdfsfrombookmarks.png)

Dividir un documento de origen basado en marcadores en varios documentos

El siguiente ejemplo es un documento DDX que utiliza marcadores para desmontar un documento de origen.

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## Determinar si los documentos son compatibles con el PDF/A {#determine-whether-documents-are-pdf-a-compliant}

Puede utilizar el servicio Assembler para determinar si un documento PDF es compatible con el PDF/A. PDF/A es un formato de archivo diseñado para la conservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

## Obtener información sobre un documento PDF {#obtain-information-about-a-pdf-document}

Puede utilizar el servicio Assembler para obtener la siguiente información sobre un documento PDF:

* Información de texto.

   * Palabras en cada página del documento
   * Posición de cada palabra en cada página del documento
   * Frases en cada párrafo de cada página del documento

* Marcadores, incluido el número de página, el título, el destino y la apariencia. Puede exportar estos\
  datos de un documento PDF e importarlos en otro PDF.

* Archivos adjuntos, incluida la información del archivo. Para los archivos adjuntos de nivel de página, también incluye la\
  ubicación de la anotación del archivo adjunto. Puede exportar estos datos desde un documento PDF e\
  Importarlos en otro PDF.

* Empaquetar archivos, incluida la información de archivo, las carpetas, el paquete, el esquema y los datos de campo. Puede exportar estos datos desde un documento PDF e importarlos en otro PDF.

## Validar documentos DDX {#validate-ddx-documents}

Puede utilizar el servicio Assembler para determinar si un documento DDX es válido. Por ejemplo, si ha actualizado desde una versión de LiveCycle anterior, la validación garantiza que el documento DDX sea válido.

## Llamar a otros servicios {#call-other-services}

Puede utilizar documentos DDX que hagan que el servicio Assembler llame a los siguientes servicios LiveC. El servicio Assembler solo puede llamar a los servicios instalados con LiveCycle.

**Servicio de extensiones de Reader**: permite a los usuarios de Adobe Reader firmar de forma digital el documento PDF resultante.

**Servicio de Forms**: combina un archivo XDP y un archivo de datos XML para producir un documento PDF que contenga el formulario interactivo rellenado.

**Servicio de salida**: convierte un formulario XML dinámico en un documento PDF que contiene un formulario no interactivo (aplana el formulario). El servicio Assembler aplana los formularios XML estáticos y los formularios Acrobat sin llamar al servicio Output.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

El uso de DDX y del servicio Assembler para llamar a otros servicios de ciclo LiveC puede simplificar el diagrama de proceso. Incluso puede reducir el esfuerzo que invierte en personalizar los flujos de trabajo. (Consulte también )
