---
title: Tipos de certificados utilizados por las extensiones de Acrobat Reader DC
description: Obtenga información acerca de los tipos de certificados utilizados por las extensiones de Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 4%

---

# Tipos de certificados utilizados por las extensiones de Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

El Visor de certificados proporciona la siguiente información sobre el certificado:

* Nombre &quot;descriptivo&quot; del certificado
* Perfiles de certificado
* Período de validez
* Derechos de uso de extensiones de Acrobat Reader DC

## Nombre &quot;descriptivo&quot; del certificado {#certificate-friendly-name}

El nombre &quot;descriptivo&quot; de un certificado de extensiones de Acrobat Reader DC es una cadena que describe las propiedades del certificado, como en el siguiente ejemplo:

SON 2D código de barras de producción completa V6.1 P8 0002054

La cadena contiene los siguientes elementos:

**Tipo de certificado:** Describe los módulos de formularios AEM que activa el certificado y el nivel de activación, como son código de barras 2D completo. Para obtener una lista de los tipos de certificado disponibles, consulte la columna Tipo en la tabla de la sección Perfiles de certificado.

**Tipo de implementación:** Indica el uso previsto del certificado, como Producción. El valor puede ser Evaluación o Producción. Para obtener una lista de los tipos de implementación asociados a cada tipo de certificado, consulte la columna Tipo de implementación en la tabla de la sección Perfiles de certificado.

**Versión de derechos de uso:** Describe la versión del algoritmo de derechos de uso para la que se puede usar el certificado, como V6.1. Esta versión no indica la versión de las extensiones de Acrobat o Acrobat Reader DC.

**Código de perfil:** El código de perfil es una descripción abreviada de las propiedades completas del certificado, como por ejemplo, P8. Para obtener una lista de los códigos de perfil asociados a cada tipo de archivo, consulte la columna Código de perfil en la tabla de la sección Perfiles de certificado.

**Número de serie:** Se asigna un número de serie a cada certificado emitido por Adobe, como 0002054. Adobe Enterprise Support o un representante de cuentas de Adobe Enterprise pueden utilizar este número de serie para rastrear el certificado a un pedido de producto específico o a una relación OEM.

## Perfiles de certificado {#certificate-profiles}

En la tabla siguiente se enumeran los perfiles de certificado que pueden encontrarse al analizar los certificados de extensiones de Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Código de perfil</p></th>
   <th><p>Tipo</p></th>
   <th><p>Período de validez</p></th>
   <th><p>Tipo de implementación</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>Producción de SAP</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>Prueba interna de SAP</p></td>
   <td><p>2 años</p></td>
   <td><p>Evaluación y prueba</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensiones de Acrobat Reader DC, producción</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensiones de Acrobat Reader DC, uso interno de Adobe</p></td>
   <td><p>2 años</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensiones de Acrobat Reader DC, integración de socios</p></td>
   <td><p>2 años</p></td>
   <td><p>Evaluación y prueba</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensiones de Acrobat Reader DC, Evaluación</p></td>
   <td><p>60 días</p></td>
   <td><p>Evaluación</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, Producción</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, producción</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; puede ser utilizado por los OEM</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; puede ser utilizado por los OEM</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Solo firma; los OEM pueden utilizarla</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Solo comentarios sin conexión; los OEM pueden utilizarlos</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Sólo comentarios; los OEM pueden utilizarlos</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Permisos completos; pueden utilizarlos los OEM</p></td>
   <td><p>Máx.</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
 </tbody>
</table>

## Período de validez {#validity-period}

Los certificados de evaluación se emiten a clientes y desarrolladores para que puedan evaluar y desarrollar aplicaciones de muestra para productos. El periodo de validez de estos certificados es de entre 60 y 90 días. Caducan al final del segundo mes siguiente a la fecha de emisión.

Los certificados de integración de socios se emiten para los socios comerciales de Adobe con el fin de apoyar el desarrollo, la integración, la creación de prototipos y las demostraciones de software. Estos certificados son válidos durante dos años a partir de la fecha de emisión.

Los certificados de uso interno de Adobe se utilizan en Adobe para admitir el desarrollo, la integración, la creación de prototipos y las demostraciones de software. Estos certificados son válidos durante dos años a partir de la fecha de emisión.

Los certificados de producción se emiten para los clientes que compraron extensiones de Acrobat Reader DC. Estos certificados son válidos durante el período máximo permitido por la entidad de certificación (CA), que se muestra como *Max* en la tabla Perfiles de certificado.

## Derechos de uso de extensiones de Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Al examinar el certificado de extensiones de Acrobat Reader DC en el Visor de certificados, puede seleccionar el elemento de derechos de uso de la pestaña Detalles (si está configurado) para ver una lista desglosada de los derechos de uso de Adobe Reader que puede habilitar el certificado. Los derechos de uso habilitados en un documento en particular pueden ser un subconjunto de los habilitados por el certificado.

Si se requieren comentarios en línea en un entorno no colaborativo, póngase en contacto con el soporte técnico de Adobe para obtener más información. La propiedad Mode coincide con el tipo de implementación y es *production* o *evaluation*.

Los derechos de uso de las extensiones de Acrobat Reader DC permitidas constan de uno o más elementos específicos. Estos elementos se utilizan en diferentes combinaciones para lograr diversas funciones de productos con licencia.

<table>
 <thead>
  <tr>
   <th><p>Elemento de derechos de uso</p></th>
   <th><p>Funcionalidad habilitada en Adobe Reader al ver un documento de PDF con derechos habilitados</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Rellene los campos de formulario y guarde los archivos localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importe y exporte datos de formulario como archivos FDF, XFDF, XML y XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Agregue, cambie o elimine campos y propiedades de campo en el formulario de PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Envíe datos, por correo electrónico o sin conexión, a un servidor cuando no se esté ejecutando en una sesión del explorador.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Cree páginas a partir de páginas de plantilla dentro del mismo formulario de PDF.</p></td>
  </tr>
  <tr>
   <td><p>Firmar</p></td>
   <td><p>Firme y guarde digitalmente documentos de PDF, y borre las firmas digitales.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Crear y modificar anotaciones de documento como comentarios.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Guarde anotaciones como comentarios en un archivo de datos independiente y cargue comentarios de un archivo.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Imprimir un documento con datos de formulario con códigos de barras en un formulario no cifrado que no requiera software de servidor con licencia para descodificar.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Cargar y descargar anotaciones, como comentarios, desde y hacia un servidor de comentarios y revisiones de documentos en línea.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Conéctese a servicios web o bases de datos definidas dentro de un formulario de PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modificar objetos de archivo incrustados asociados al documento de PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los derechos de uso de las extensiones de Acrobat Reader DC solo se pueden licenciar desde Adobe en determinadas combinaciones que funcionan juntas. No es posible otorgar licencias a estas capacidades de forma independiente. Para obtener información sobre las combinaciones disponibles de derechos de uso, póngase en contacto con un representante de cuentas de formularios AEM Forms.
