---
title: Prácticas recomendadas para formularios HTML5
description: Ajuste su formulario HTML5 basado en XFA para obtener el mejor rendimiento.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 96%

---

# Prácticas recomendadas para formularios HTML5{#best-practices-for-html-forms}

## Información general {#overview}

AEM Forms tiene un componente llamado Formularios HTML5. Ayuda a procesar formularios PDF basados en XFA existentes (archivos XDP) en formato HTML5. Este documento proporciona directrices y recomendaciones para reducir el tiempo de carga y mejorar el rendimiento de los formularios HTML5 en dispositivos móviles.

La mayoría de los dispositivos móviles tienen una potencia de procesamiento y capacidades de memoria limitadas. Ayuda a mejorar el tiempo de espera de los dispositivos móviles. Los exploradores web que se ejecutan en un dispositivo móvil tienen acceso a recursos limitados (memoria limitada y capacidades de procesamiento). Una vez alcanzado el límite, el comportamiento del explorador se vuelve lento. Este documento proporciona recomendaciones para mantener el tamaño correcto de un formulario HTML5. Un formulario más pequeño no infringe los límites de memoria y potencia de procesamiento de un dispositivo y proporciona una experiencia fluida.

Las recomendaciones que se examinan en este artículo están dirigidas a los formularios HTML5, pero son igualmente aplicables a los formularios PDF basados en XFA. Estas prácticas recomendadas contribuyen colectivamente al rendimiento general de los formularios HTML5. Requiere una planificación cuidadosa para desarrollar formularios eficientes y productivos. Empecemos:

## Los nodos son la divisa de los formularios HTML5, inviértalos con prudencia {#nodes-are-currency-of-html-forms-spend-them-wisely}

Por lo general, un formulario XFA tiene varios elementos. Por ejemplo, tabla, campo de texto e imágenes. Cada elemento tiene varias propiedades para controlar el comportamiento y el aspecto del elemento. Cuando se procesa un formulario XFA en formato HTML5, todos los elementos XFA y las propiedades correspondientes se convierten en nodos Modelo o HTML DOM. Estos nodos aumentan el tamaño y la complejidad de un DOM. Y hacen que el formulario HTML5 sea lento de procesar.

Es más fácil para los exploradores procesar un DOM más ligero. Por lo tanto, puede realizar las siguientes optimizaciones en un formulario XFA para reducir el número de nodos. Genere una estructura DOM ligera:

* Utilice la propiedad caption para agregar una etiqueta a un campo. No utilice un elemento Texto independiente para agregar una etiqueta. Ayuda a reducir el peso adicional, lo que provoca mejoras en el rendimiento. También ayuda a evitar problemas de diseño.
* Mantenga al mínimo el número de elementos de texto Dibujar de un formulario. Los elementos Dibujar son útiles para mejorar la legibilidad y la apariencia, pero no tienen ninguna capacidad de almacenamiento de información. Se recomienda combinar varios elementos de texto Dibujar en uno solo. Utilice todas sus opciones para hacer el formulario más ligero.

## Los formularios Lite funcionan mejor, mantienen los recursos comprimidos {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulario HTML5 puede contener varios recursos externos, como archivos de imagen, JavaScript y CSS. Cada vez que un explorador solicita un formulario, los recursos externos se envían a través de la red. El tiempo necesario para viajar por la red es directamente proporcional al tamaño de los archivos.

Por lo tanto, reducir el tamaño de los recursos externos y utilizar solo los recursos absolutamente necesarios es el método preferido para mejorar el rendimiento de los formularios. Puede realizar las siguientes optimizaciones en un formulario XFA para reducir el tamaño de los recursos externos:

* Usar [imágenes comprimidas](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Reduce la actividad de red y la cantidad de memoria necesaria para procesar un formulario. Por lo tanto, el tiempo de carga del formulario disminuye sustancialmente.
* Utilizar la opción minificar en el Administrador de configuración de AEM (Administrador de bibliotecas HTML Day CQ) para comprimir archivos JavaScript y CSS. Para obtener más información, consulte [Ajustes de la configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Habilitar la compresión web. Reduce el tamaño de las solicitudes y respuestas originadas desde un formulario. Para obtener más información, consulte [Ajuste del rendimiento de AEM Forms Server](https://helpx.adobe.com/es/aem-forms/6-3/performance-tuning-aem-forms.html).

## Mantener vivo el interés, mostrar solo los campos obligatorios  {#keep-the-interest-alive-show-only-required-fields}

Un formulario HTML5 puede tener cientos de páginas. Un formulario con un gran número de campos es lento de cargar en el explorador. Puede realizar las siguientes optimizaciones en un formulario XFA para optimizar los formularios con un gran número de campos y páginas:

* Evaluar la división de los formularios grandes en varios formularios. También puede utilizar un conjunto de formularios para agrupar todos los formularios más pequeños y presentarlos como una sola unidad. Un conjunto de formularios solo carga los formularios necesarios. Además, en un conjunto de formularios, se pueden configurar campos comunes en distintos formularios para compartir enlaces de datos. Los enlaces de datos ayudan a los usuarios a rellenar la información común solo una vez; la información se rellenará automáticamente en formularios posteriores, lo que supone mejoras sustanciales del rendimiento. Para obtener más información sobre los conjuntos de formularios, consulte [Conjuntos de formularios en AEM Forms](https://helpx.adobe.com/es/aem-forms/6-3/formset-in-aem-forms.html).
* Considere la posibilidad de dividir secciones y mover cada sección a una página diferente. Los formularios HTML5 se cargan dinámicamente en cada página en la solicitud de desplazamiento de la página. Solo la página desplazada (la página que se muestra y las que la preceden) se almacenan en la memoria; el resto de las páginas se cargan bajo demanda. Por lo tanto, dividir y mover una sección en una página por su cuenta reduce el tiempo necesario para cargar un formulario. También puede utilizar la primera página del formulario como página de aterrizaje. Es similar a la tabla de contenidos (TOC) de un libro. Una página de aterrizaje de un formulario solo contiene vínculos a las demás secciones del formulario. Mejora significativamente el tiempo de carga de la primera página del formulario y mejora la experiencia del usuario.
* Mantenga las secciones condicionales ocultas de forma predeterminada. Consiga que estas secciones solo sean visibles cuando se cumpla una determinada condición. Ayuda a reducir al mínimo el tamaño del DOM. También puede utilizar la navegación con pestañas para mostrar solo una sección a la vez.

## Menos es más, reduzca el número de páginas {#less-is-more-reduce-the-number-of-pages}

Los formularios HTML5 pueden contener campos impulsados por datos (tablas y subformularios). Estos campos amplían el tamaño del formulario en tiempo de ejecución. Por ejemplo, una tabla controlada por datos en un formulario HTML5 puede abarcar hasta miles de filas. Estas tablas pueden causar una degradación del diseño y del rendimiento. Las optimizaciones sugeridas a continuación pueden ayudarle a reducir el tiempo de carga de los formularios HTML5 con campos impulsados por datos:

* Utilice scripts XFA para lograr que la navegación por páginas muestre campos impulsados por datos (tablas y subformularios). En la navegación por páginas, solo se muestran datos específicos en una página. Limita la operación paint del explorador a los campos que se muestran a la vez y facilita el desplazamiento por el formulario. Además, los usuarios de los dispositivos móviles solo están interesados en un subconjunto de datos. Le ayuda a ofrecer una buena experiencia de usuario y a reducir el tiempo necesario para cargar los datos necesarios. Se obtienen dos soluciones por el precio de una.  Tenga en cuenta también que la navegación por páginas no está disponible de forma predeterminada. Puede utilizar scripts XFA para desarrollar la navegación por páginas.

* Evalúe la combinación de varias columnas de solo lectura en una sola columna. Reduce la memoria necesaria para mostrar el formulario. Además, evite mostrar las columnas que no requieran ninguna entrada de los usuarios.
* Evaluar la división del formulario basado en datos en un [conjunto de formularios](https://helpx.adobe.com/es/aem-forms/6-3/formset-in-aem-forms.html), si las sugerencias anteriores no le proporcionan muchas mejoras. Por ejemplo, si una tabla tiene más de 1000 filas, mueva cada 100 filas a un formulario diferente. Ayudaría a mejorar el tiempo de carga y el rendimiento de los formularios. Tenga en cuenta también que un conjunto de formularios genera un XML de envío consolidado para todos los formularios. Para diferenciar los datos de cada formulario, utilice diferentes fuentes de datos. Para obtener más información, consulte [Conjunto de formularios en AEM Forms](https://helpx.adobe.com/es/aem-forms/6-3/formset-in-aem-forms.html).

## Poder de dos para Documentos de registro (DOR) {#power-of-two-for-document-of-record-dor}

Un formulario XFA puede tener un gran número de secciones dedicadas únicamente a Documentos de registro (DOR). Para reducir el número de nodos y mejorar el rendimiento de un formulario de este tipo, puede mantener diferentes copias del formulario: una para rellenar el formulario y otra para generar el documento de registro en el servidor. En la copia para rellenar el formulario XFA, se muestran los campos requeridos solo para capturar datos. En el formulario Generar documento de registro XFA, mantenga los campos requeridos solamente en la salida impresa del formulario. Antes de elegir el enfoque sugerido, evalúe la ganancia de rendimiento y la sobrecarga de mantenimiento.

## Lecturas recomendadas  {#recommended-reads}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales simples y atractivas. Pero desarrollar formas eficientes y productivas requiere un esfuerzo concertado. Además de formularios HTML5, estas son algunas lecturas recomendadas para prácticas recomendadas generales de AEM:

* [Prácticas recomendadas para implementar y mantener AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas para crear contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas para la administración de AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas para desarrollar soluciones](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas para usar formularios adaptables ](/help/forms/using/adaptive-forms-best-practices.md)
* [El servidor de AEM Forms no incrusta las fuentes en un formulario PDF dinámico](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Tarjeta de referencia rápida {#quick-reference-card}

Puede imprimir la siguiente tarjeta (haga clic en tarjeta para descargar una versión de alta resolución) y mantenerla en su escritorio para una referencia rápida:
[![Tarjeta de referencia rápida de las prácticas recomendadas de HTMLForms 5](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
