---
title: Iniciar las API de Document Services desde el flujo de trabajo de AEM
description: Aprenda a invocar AEM Document Services en DDX o en las entradas suministradas. Consulte también Cómo convertir PDF a PDF/A
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 92%

---

# Iniciar las API de Document Services desde el flujo de trabajo de AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

AEM Forms proporciona flujos de trabajo personalizados para invocar las siguientes API del servicio Assembler:

* **invoke**: invoca operaciones especificadas en una entrada DDX en las entradas suministradas.
* **toPDFA**: convierte el documento PDF de entrada en un documento PDF/A.

### Invocar un flujo de trabajo DDX {#invoke-ddx-workflow}

El flujo de trabajo **Invocar DDX** invoca la API del servicio Assembler`Invoke`, que puede utilizar para ensamblar o desmontar documentos, agregar marcas de agua a un PDF, etc.

1. Arrastre el paso de flujo de trabajo **[!UICONTROL Invocar DDX]** a la pestaña Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, las opciones del entorno y los documentos de salida, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents}

El flujo de trabajo Invocar DDX requiere los siguientes documentos de entrada:

* **DDX**: es una entrada obligatoria para el paso de flujo de trabajo Invocar DDX, y se puede especificar seleccionando una de las siguientes opciones en la lista desplegable de la entrada DDX.

   * *Relativo a carga útil*: el archivo de entrada DDX es relativo a la carpeta de carga útil del elemento de flujo de trabajo.
   * *Usar carga útil*: la carga útil del elemento de flujo de trabajo se utiliza como documento DDX de entrada.
   * *Ruta absoluta*: la ruta absoluta del documento DDX en el repositorio CRX.

* **Crear mapa a partir de carga útil**: cuando se selecciona, todos los documentos de la carpeta de carga útil se agregan al mapa del documento de entrada para la API `invoke` en Assembler. El nombre de nodo de cada documento se utiliza como clave en el mapa.

* **Mapa del documento de entrada**: especifica el mapa del documento de entrada. Puede agregar cualquier número de entradas, y cada una especifica la clave del documento en el mapa y el origen del documento.

#### Opciones de entorno {#environment-options}

La pestaña Opciones de entorno le permite establecer varias opciones de procesamiento para la API de invocación.

* *Nivel de registro de trabajo*: especifica el nivel de registro para los registros de procesamiento.
* *Validar solo*: comprueba la validez del DDX de entrada.

* *Fallo al producirse el error*: especifica si la llamada al servicio Assembler debe fallar en caso de error. El valor predeterminado es False.

#### Documentos de salida {#output-documents}

En función del DDX de entrada, la API de invocación puede producir varios documentos de salida. La pestaña Documentos de salida permite seleccionar dónde se guardará el documento de salida.

1. *Guardar salida en carga útil*: guarda los documentos de salida en la carpeta de carga útil o sobrescribe la carga útil, en el caso de que esta sea un archivo.
1. *Mapa del documento de salida*: le permite especificar explícitamente dónde guardar cada documento de salida agregando una entrada por documento. Cada entrada especifica el documento y la ubicación de guardado. Un documento de salida puede sobrescribir la carga útil o guardarse en la carpeta de carga útil. Resulta útil cuando hay varios documentos de salida.

1. *Registro de trabajo*: especifica dónde guardar el documento de registro de trabajo, lo que resulta útil para solucionar errores.

### Flujo de trabajo Convertir a PDF/A {#convert-to-pdf-a-workflow}

El paso de flujo de trabajo Convertir en PDF/A invoca la API del servicio Assembler `toPDFA`. Se utiliza para convertir documentos PDF en documentos compatibles con el estándar PDF/A.

1. Arrastre el paso de flujo de trabajo **[!UICONTROL ConvertToPDFA]** a la pestaña Forms Workflow de la barra de tareas.

1. Haga doble clic en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, las opciones de conversión y los documentos de salida, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-1}

Especifique el origen del documento para convertirlo en un documento compatible con el estándar PDF/A de una de las siguientes formas.

* *Relativo a carga útil*: el documento de entrada es relativo a la carpeta de carga útil del elemento de flujo de trabajo.
* *Usar carga útil*: la carga útil del elemento de flujo de trabajo se utiliza como documento de entrada.
* *Ruta absoluta*: la ruta absoluta del documento de entrada en el repositorio CRX.

#### Opciones de conversión {#conversion-options}

Las opciones de conversión permiten especificar opciones que modifican el proceso de conversión de PDF/A.

* *Cumplimiento*: especifica el estándar PDF/A que debe cumplir el PDF/A de salida.
* *Nivel de resultado*: especifica el nivel de registro que se utilizará para los registros de conversión del PDF/A.
* *Firmas*: especifica cómo se deben procesar las firmas del documento de entrada durante la conversión.
* *Espacio de color*: especifica el espacio de color predefinido que se utilizará para el documento PDF/A de salida.
* *Verificar* conversión: especifica si el documento PDF/A convertido debe verificarse para que sea compatible con el estándar PDF/A después de la conversión.
* *Nivel de registro de trabajo*: especifica el nivel de registro que se utilizará para procesar los registros.

* *Esquema de extensión de metadatos*: especifica la ruta del esquema de extensión de metadatos que se utilizará para las propiedades XMP de los metadatos del documento PDF.

#### Documentos de salida {#output-documents-1}

La pestaña Documentos de salida permite especificar el destino de los documentos de salida

* *Documento PDF/A*: especifica la ubicación en la que se guarda el documento PDF/A convertido. Puede sobrescribir el documento de carga útil o guardarse en la carpeta de carga útil.
* *Registro de conversión*: especifica la ubicación en la que se guardan los registros de conversión. Puede sobrescribir el documento de carga útil o guardarse en la carpeta de carga útil.

## Forms {#forms}

El flujo de trabajo Procesar formulario PDF es un contenedor de la API del servicio Forms `renderPDFForm` para crear un formulario de PDF utilizando una plantilla XDP y un XML de datos.

### Procesar formulario PDF {#render-pdf-form-workflow}

1. Arrastre el paso de flujo de trabajo Procesar formulario PDF a la pestaña Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, los documentos de salida y los parámetros adicionales, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-2}

* *Archivo de plantilla*: especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento de datos*: especifica la ubicación del XML de datos que debe combinarse con la plantilla.

#### Documentos de salida {#output-documents-2}

* *Documento de salida*: especifica el nombre del formulario PDF generado.

#### Parámetros adicionales {#additional-parameters}

* *Raíz de contenido*: especifica la ruta de la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *URL de Envío*: especifica la URL de envío predeterminada para el formulario PDF generado.
* *Configuración regional*: especifica la configuración regional predeterminada para el formulario PDF generado.
* *Versión de Acrobat*: especifica la versión de Acrobat de destino del formulario PDF generado.
* *PDF etiquetado*: especifica si se debe hacer accesible el PDF generado.
* *Documento XCI*: especifica la ruta del archivo XCI.

## Salida {#output}

El flujo de trabajo Generar PDF no interactivo es un contenedor de la API del servicio Output `generatePDFOutput`. Se utiliza para generar documentos PDF no interactivos a partir de la plantilla XDP y el XML de datos.

### Flujo de trabajo Generar salida PDF no interactiva   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arrastre el flujo de trabajo Generar salida PDF no interactiva a la pestaña Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, los documentos de salida y los parámetros adicionales, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-3}

* *Archivo de plantilla*: especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento de datos*: especifica la ubicación del XML de datos que debe combinarse con la plantilla.

#### Documento de salida {#output-document}

*Documento de salida*: especifica el nombre del formulario PDF generado.

#### Parámetros adicionales {#additional-parameters-1}

* *Raíz de contenido*: especifica la ruta de la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *Configuración regional*: especifica la configuración regional predeterminada para el formulario PDF generado.
* *Versión de Acrobat*: especifica la versión de Acrobat de destino del formulario PDF generado.
* PDF linearizado: especifica si se debe optimizar el PDF generado para la visualización web.
* *PDF etiquetado*: especifica si se debe hacer accesible el PDF generado.
* *Documento XCI*: especifica la ruta del archivo XCI.
