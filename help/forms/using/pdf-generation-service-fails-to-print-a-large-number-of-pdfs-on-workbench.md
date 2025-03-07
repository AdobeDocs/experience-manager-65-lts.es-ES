---
title: La generación de PDF no puede imprimir un gran número de PDF con Workbench
description: Cuando un cliente genera un gran número de PDF a través de servicios implementados mediante Workbench, el servicio de impresión falla.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 80a4e5c0-d68f-4591-a43d-ab75b5f0764c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# La generación de PDF no puede imprimir un gran número de PDF a través de Workbench {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## Problema {#issue}

Cuando un cliente genera un gran número de PDF a través de servicios implementados mediante Workbench. El servicio falla debido a que no hay memoria suficiente. El error se muestra como:

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

Esto se debe a que el número máximo de páginas en una solicitud de impresión está limitado a aproximadamente 1000 páginas en Windows. Cuando se genera una salida de impresión, es necesario cargar la plantilla y los datos en la memoria y el diseño resultante se crea en la memoria. Esto significa que el tamaño de la salida final tiene límites. El proceso que genera la salida de impresión es una tarea de 32 bits, lo que significa que está limitada a 2 GB de RAM en Windows <!--and 4 GB on UNIX-->.

## Se aplica a {#applies-to}

La solución se aplica a AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> para x86_win32 XMLFM.

## Solución {#solution}

El factor más grande que afecta al uso de la memoria es la cantidad de datos de un formulario. Sin embargo, hay otros factores en un diseño de formulario que afectan en menor medida al uso de la memoria. Cuando tenga en cuenta estos factores, puede diseñar un formulario para una salida de impresión más grande. La siguiente sección indica, en orden de prioridad, los factores que influyen en el espacio de memoria:

### Factor de impacto {#impact-factor}

**Alta**

1. **Subformularios de opción**: un conjunto de subformularios de opción es una variación del objeto del conjunto de subformularios que le permite personalizar la visualización de subformularios específicos desde el conjunto mediante instrucciones condicionales.
1. **Usar texto estático en lugar de subtítulos**: casi todos los campos proporcionan un subtítulo dentro de, el usuario debe utilizarlo en lugar de tener un texto estático adicional como subtítulo.
1. Utilice **formato de texto enriquecido (RTF)** siempre que sea posible.

**Promedio**

Factores adicionales que se deben tener en cuenta al diseñar la plantilla de formulario para ayudar a mejorar el uso de la memoria:

1. Evite utilizar texto estático para etiquetar un campo. En su lugar, utilice subtítulos en el campo de texto.
2. No utilice en exceso rectángulos, líneas, objetos y tablas.
3. Evite utilizar subformularios de texto enriquecido y de opciones, si es posible.
4. Evite el uso excesivo de subformularios y subformularios anidados.

### Limitación de tamaño de datos {#data-size-limitations}

Como estamos limitados por la memoria de proceso máxima y la memoria consumida por el proceso no solo depende del tamaño del archivo de datos. Está muy estrechamente relacionado con el diseño de formulario y, en cierta medida, con la cantidad real de datos que se combinan en el formulario.

Si el formulario tiene muchos nodos pequeños con datos pequeños, el proceso consume más memoria (y, por lo tanto, se queda sin memoria más rápido) que un formulario que tiene menos nodos (incluso) con datos grandes.

Lea el [Apéndice siguiente](#appendix) para obtener más información, donde los resultados de las pruebas se basan en Imprimir formulario (PDF no etiquetado). El uso de PDF etiquetados aumenta los requisitos de memoria de proceso. También depende del número de campos del formulario: aproximadamente, el requisito de memoria de proceso sería algo más de 1,5 veces el de PDF no etiquetado.

### Forms interactivo {#interactive-forms}

Los formularios interactivos consumirían más memoria que Imprimir Forms a medida que se vuelvan a procesar los campos interactivos. En las pruebas realizadas, el consumo de memoria se incrementó en un factor de 1,5 aproximadamente en comparación con los formularios impresos y estos fueron formularios interactivos estáticos.

### Formatos de imagen {#image-formats}

Adobe no recomienda ningún formato de imagen específico. Pero sería bueno tener un tamaño de imagen más pequeño, por ejemplo, PNG (Portable Network Graphics). Tampoco es aconsejable utilizar imágenes de alta resolución cuyos tamaños varían varios cientos de MegaBytes. Además, no es aconsejable utilizar imágenes comprimidas cuyo tamaño tras la descompresión se expanda a varios cientos de Megabytes de datos.

### Apéndice {#appendix}

**Ejemplos de tablas**

A continuación se muestran diferentes variantes para tablas que muestran el número de páginas representadas en comparación con el tamaño de los datos para tablas simples y tablas complejas.

1. Una tabla con una sola columna en la que se generan 5000 páginas de PDF, con un tamaño de archivo de datos de 24 MB y registros de 30 KB.

   ![tabla_columna_única](/help/forms/using/assets/table_single_column.png)

1. Una tabla con muchas columnas pequeñas donde se generan 800 páginas de PDF, el tamaño del archivo de datos es de 4,6 MB y registros de 20-K.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. Una tabla con muchas columnas pequeñas, pero un archivo de datos más grande debido al uso de nombres xmlTag más grandes.
En este caso, todo es igual que el anterior, pero los nombres de etiquetas xml se han hecho grandes (por lo que el tamaño del archivo de datos aumentará sin ningún aumento en los datos efectivos reales), el resultado final (límite superior) es casi el mismo. Aunque el tamaño del archivo de datos aumentó de 4,6 MB a 44,6 MB. Aquí se generan 800 páginas de PDF, el tamaño del archivo de datos es de 44,6 MB y los registros de 20-K.

   ![nombre_etiqueta_xml_table_greater_table](/help/forms/using/assets/table_bigger_xml_tagname.png)

Por lo tanto, es difícil establecer un límite superior general en el tamaño del archivo de datos. Cada formulario es único y, por lo tanto, el consumo de memoria diferiría de una forma a otra.
