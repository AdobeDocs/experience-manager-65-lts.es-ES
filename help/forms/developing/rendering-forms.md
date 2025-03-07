---
title: Representar formularios
description: Utilice el servicio Forms para crear aplicaciones cliente de captura de datos interactivas que validen, procesan, transforman y envían formularios creados normalmente en Designer. Los autores de formularios pueden desarrollar un único diseño de formulario que el servicio Forms procesa en PDF, SWF o HTML en varios entornos de explorador.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 3f1f9ecb-be62-4428-8db8-23c57081b0f7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Representar formularios {#rendering-forms}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Forms**

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios creados normalmente en Designer. Los autores de formularios pueden desarrollar un único diseño de formulario que el servicio Forms procesa en PDF, SWF o HTML en varios entornos de explorador.

Cuando un usuario final solicita un formulario, una aplicación cliente envía la solicitud al servicio de Forms, que lo devuelve en un formato adecuado. En cuanto el servicio Forms recibe una solicitud, combina los datos con un diseño de formulario y, a continuación, envía el formulario en el formato deseado. La salida del servicio de Forms es un formulario interactivo, normalmente un documento de PDF. Un formulario interactivo permite a los usuarios rellenar campos ubicados en el formulario.

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web cliente o guardarlo como archivo PDF. Una aplicación basada en web puede escribir el formulario en un explorador web. Una aplicación de escritorio puede guardar el formulario como un archivo PDF. Para mostrar cómo escribir en un explorador web y en un archivo PDF, los inicios rápidos de la sección *Rendering Forms* se organizan de la siguiente manera:

* Los ejemplos de API de Java con establecimiento inflexible de tipos (modo SOAP) son un servlet Java.
* Los ejemplos del servicio web (Java Base64) son un servlet Java.
* Los ejemplos del servicio web (MTOM) son una aplicación de consola (no todos los inicios rápidos tienen un ejemplo de MTOM).

>[!NOTE]
>
>Para obtener información sobre cómo crear una aplicación web que use servlets java para invocar el servicio Forms, consulte [Creación de aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Puede pasar un diseño de formulario (un archivo XDP) o un documento de PDF al servicio Forms de una de las dos maneras siguientes:

* Puede hacer referencia al diseño de formulario mediante un valor de URL. Este método implica el uso de un objeto `URLSpec`. La raíz de contenido se pasa al servicio Forms mediante el método `setContentRootURI` del objeto `URLSpec`. El nombre del diseño del formulario ( `formQuery`) se pasa como parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario. (La mayoría de los inicios rápidos de la sección *Renderización de Forms* utilizan este método).
* Puede pasar un(a) `com.adobe.idp.Document` que contenga el diseño de formulario al servicio Forms. Dos nuevos métodos denominados `renderPDFForm2` y `renderHTMLForm2` aceptan un objeto `com.adobe.idp.Document` que contiene un diseño de formulario. (Ver [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

Puede realizar estas tareas mediante el servicio Forms:

* Procesar PDF forms interactivo. (Consulte [Procesamiento de PDF forms interactivo](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Procesar formularios en el cliente. (Consulte [Renderización de Forms en el cliente](/help/forms/developing/rendering-forms-client.md)).
* Procesar formularios basados en fragmentos (Consulte [Procesar Forms basado en fragmentos](/help/forms/developing/rendering-forms-based-fragments.md)).
* Procesar formularios con derechos activados. (Consulte [Forms con derechos de procesamiento habilitados](/help/forms/developing/rendering-rights-enabled-forms.md)).
* Procesar formularios como HTML. (Consulte [Procesar Forms como HTML](/help/forms/developing/rendering-forms-html.md)).
* Procesar HTML Forms con archivos CSS personalizados ([Procesar HTML Forms con archivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Administrar formularios enviados. (Consulte [Gestión de Forms enviados](/help/forms/developing/handling-submitted-forms.md).)
* Crear documentos PDF con datos XML enviados. (Consulte [Creación de documentos de PDF con datos XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md)).
* Rellenar previamente formularios. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
* Pasar documentos. (Ver [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcular datos de formulario. (Consulte [Cálculo de datos de formulario](/help/forms/developing/calculating-form-data.md).)
* Optimizar una aplicación. (Consulte [Optimización del rendimiento del servicio Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
