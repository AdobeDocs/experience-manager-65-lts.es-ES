---
title: Servicio de Forms
description: El artículo describe el servicio Forms y las tareas relacionadas con los formularios que puede realizar mediante este servicio.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 100%

---

# Servicio de Forms {#forms-service}

## Información general {#overview}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios que normalmente se crean en Designer. El servicio Forms procesa como un documento PDF cualquier diseño de formulario que desarrolle.

También permite a las organizaciones ampliar sus procesos inteligentes de captura de datos mediante la implementación de formularios electrónicos como PDF de Adobe. Asimismo, puede utilizar el servicio para importar y exportar datos procedentes y destinados a formularios PDF existentes, respectivamente.

Utilice el servicio Forms para realizar las siguientes tareas:

* Procesar formularios PDF basados en plantillas y datos XML
* Habilitar la integración de datos de formulario para importar datos en formularios PDF y extraer datos de ellos
* Procesar formularios basados en fragmentos

## Creación de formularios PDF  {#creating-pdf-forms-nbsp}

Utilice el servicio de Forms para crear formularios PDF para capturar datos. Normalmente, el proceso se inicia con una plantilla de AEM Forms Designer. Utilice la operación `renderPDFForm` (vínculo a Javadoc) del servicio Forms para convertir esta plantilla en un formulario PDF.

El primer parámetro de la operación `renderPDFForm` es el nombre del archivo de plantilla (por ejemplo, `ExpenseClaim.xdp`). Puede almacenar el archivo de plantilla en un sistema de archivos local, un repositorio CRX o una ubicación HTTP o FTP. Puede especificar la ubicación del archivo de plantilla estableciendo la raíz de contenido en el parámetro `PDFFormRenderOptions` de la operación `renderPDFForm`. Consulte Javadoc para obtener más información sobre el resto de opciones que puede especificar para el parámetro `PDFFormRenderOptions`.

La operación `renderPDFForm` también puede aceptar datos XML. Los datos XML se combinan con la plantilla al crear un formulario PDF, de forma que el formulario PDF generado contiene los datos especificados. El segundo parámetro de la operación `renderPDFForm` puede aceptar un objeto Document (Javadoc) que contenga datos XML.

## Extracción de datos de formularios PDF  {#extracting-data-from-pdf-forms-nbsp}

Utilice la operación `exportData` (Javadoc) del servicio Forms para extraer datos XML de un formulario PDF. Esta operación acepta un documento como primer parámetro. Puede exportar los datos como un documento XDP o como un archivo XML. Si exporta los datos como un archivo XML, los datos exportados quitan el sobre XDP y devuelven un archivo XML sin formato. Puede especificar esta disposición con el segundo parámetro.

## Importación de datos en formularios PDF {#importing-data-into-pdf-forms}

El servicio Forms también permite combinar un formulario PDF creado mediante AEM Forms Designer o la operación `renderPDFForm` con datos XML. La operación `importData` (Javadoc) del servicio Forms acepta el formulario PDF y los datos XML y devuelve un formulario PDF con datos XML.

## Procesamiento de formularios basados en fragmentos {#rendering-forms-based-on-fragments}

El servicio Forms puede procesar formularios basados en fragmentos creados con AEM Forms Designer. Un fragmento es una parte reutilizable de un formulario. Se guarda como un archivo XDP independiente que se puede insertar en varios diseños de formulario. Por ejemplo, un fragmento puede incluir un bloque de direcciones o texto legal.

El uso de fragmentos simplifica y acelera la creación y el mantenimiento de una gran cantidad de formularios. Cuando crea un formulario, puede insertar una referencia al fragmento necesario para que este aparezca en el formulario. La referencia de fragmento contiene un subformulario que señala al archivo XDP físico.

Estas son las ventajas de utilizar fragmentos:

* **Reutilización de contenido**: puede reutilizar contenido en diferentes diseños de formulario. Para reutilizar rápidamente partes del mismo contenido en varios formularios, cree un fragmento. Copiar o volver a crear el contenido lleva más tiempo. El uso de fragmentos también garantiza que el contenido y el aspecto de las partes de un diseño de formulario que se utilizan con frecuencia sean coherentes en todos los formularios de referencia.
* **Actualizaciones globales**: puede realizar cambios globales en varios formularios modificando un archivo una única vez. Puede cambiar el contenido, los objetos de script, los enlaces de datos, el diseño o los estilos de un fragmento. Los cambios se reflejarán en todos los formularios XDP que hagan referencia a ese fragmento.
* **Creación de formularios compartidos**: puede compartir la creación de formularios entre varios recursos. Los desarrolladores de formularios con conocimientos de scripts u otras funciones avanzadas de AEM Forms Designer pueden desarrollar y compartir fragmentos que utilizan scripts y propiedades dinámicas. Los diseñadores de formularios pueden utilizar los fragmentos para diseñar formularios. Asimismo, pueden utilizar fragmentos para asegurarse de que todas las partes de un formulario tienen un aspecto y una funcionalidad coherentes en todos los formularios.
