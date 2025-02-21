---
title: Medir y mejorar la eficacia y la conversión de formularios
description: AEM Forms se integra con las soluciones Adobe Target y Adobe Analytics, lo que le permite medir y mejorar el rendimiento y la tasa de conversión de los formularios.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 94%

---

# Medir y mejorar la eficacia y la conversión de formularios{#measure-and-improve-effectiveness-and-conversion-of-forms}

## El reto {#the-challenge-br}

Las organizaciones permiten y animan cada vez más a sus clientes a realizar transacciones mediante autoservicios digitales a través de múltiples canales. Sin embargo, dado que carecen de un mecanismo de comentarios uno a uno, es difícil medir el éxito y experimentar con los formularios digitales para mejorar la experiencia del cliente y aumentar las conversiones.

Para maximizar el ROI, las organizaciones deben monitorizar cómo sus clientes interactúan con los servicios y experimentar con los artefactos digitales (formularios) para mejorar su experiencia. Para medir el éxito y definir una estrategia de mejora, las organizaciones necesitan respuestas a preguntas como las siguientes:

* ¿Cuántos clientes han intentado acceder o realizar transacciones con mis formularios?
* ¿Cuántos de ellos completaron correctamente la transacción?
* ¿Cuántos abandonaron el formulario?
* ¿Cuáles son las áreas problemáticas en las que los clientes tienen dificultades?
* ¿Qué cambios debo realizar y cómo puedo probar cuáles mejoran las conversiones?

## La solución {#the-solution}

AEM Forms se integra con las soluciones de [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluciones [Adobe Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html) y [Adobe Target](https://www.adobe.com/es/marketing-cloud/testing-targeting.html), lo cual le permite supervisar y analizar el rendimiento de los formularios, así como experimentar e identificar la experiencia que proporciona una mejor tasa de conversión.

## El flujo de trabajo {#the-workflow}

Vamos a ver con más detalle cómo medir el rendimiento y mejorar las tasas de conversión de los formularios.

### Audiencia objetivo {#target-audience}

* Usuarios y analistas empresariales responsables de las estrategias de marketing y éxito
* Personal de TI encargado de la configuración y el mantenimiento de la infraestructura y las soluciones

### Componentes y funciones de AEM Forms utilizados {#aem-forms-components-and-features-involved}

* Formularios adaptables
* Integración con Adobe Analytics para recopilar, organizar y crear informes sobre las interacciones de los clientes con los formularios adaptables
* Integración con Adobe Target para ejecutar pruebas A/B en formularios adaptables

### Suposiciones {#assumptions}

* Ya tiene una cuenta de Adobe Marketing Cloud y se ha registrado en las soluciones Analytics y Target.
* Ha publicado un formulario adaptable al que los clientes pueden acceder.

### Pasos del flujo de trabajo {#workflow-steps}

#### Paso 1: Configuración de Analytics y Target en AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar Analytics**

Para obtener información más detallada sobre las interacciones de los clientes con los formularios, primero debe configurar Analytics en AEM Forms. Siga estos pasos:

1. Cree un grupo de informes en Adobe Analytics.
1. Cree la configuración de Cloud Service en AEM.
1. Cree el marco de Cloud Service en AEM.
1. Configure el servicio de configuración de AEM Forms Analytics en AEM.
1. Active el análisis en el formulario de AEM.

Para ver los pasos detallados, consulte [Configuración de análisis e informes para formularios adaptables](../../forms/using/configure-analytics-forms-documents.md).

**Configuración de Target**

Para crear y ejecutar pruebas A/B en los formularios adaptables, configure Target en AEM Forms como se describe en [Configuración e integración de Target en AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Paso 2: Ver el informe de análisis {#step-view-analytics-report-br}

A medida que sus clientes acceden a los formularios en los que ha activado Analytics e interactúan con ellos, sus interacciones se capturan en bases de datos de Analytics de alta seguridad. Los clientes segmentan las bases de datos, y es posible acceder a ellas a través de conexiones seguras.

Puede ver los informes de los formularios en los que ha activado el análisis y analizar los datos en AEM. Para ver el informe:

1. En el servidor de AEM, vaya a **Forms > Formularios y documentos**.
1. Seleccione el formulario en el que desea realizar el informe de análisis.
1. Haga clic en el icono Informes de Analytics. Se mostrará el informe.

Vamos a echar un vistazo a los puntos de datos que Analytics recopila e incluye en los informes de los formularios.

**Informe de análisis de Forms**

El informe de análisis de los formularios adaptables captura los siguientes indicadores clave de rendimiento (KPI) a nivel de formulario:

* **Promedio de tiempo de llenado**: el tiempo promedio empleado en rellenar el formulario.
* **Impresiones**: el número de veces que el formulario ha aparecido en los resultados de búsqueda.

* **Representaciones**: el número de veces que se ha representado o abierto el formulario.
* **Borradores**: el número de veces que el formulario se ha guardado como borrador.

* **Envíos**: el número de veces que se ha enviado el formulario.
* **Cancelaciones**: el número de veces que los usuarios han abandonado el formulario sin completarlo.
* **Visitas/envíos**: la proporción de visitas por envío.

Asimismo, obtiene los siguientes detalles sobre cada uno de los paneles del formulario:

* **Tiempo**: el tiempo promedio empleado (en segundos) en el panel y sus campos.

* **Errores**: el número de errores encontrados en el panel y sus campos por cada 1000 representaciones del formulario.

* **Ayuda**: el número de veces que los usuarios han accedido a la ayuda en contexto del panel y sus campos por cada 1000 representaciones del formulario

![Informe de análisis de ejemplo de un formulario adaptable](assets/summary-report.png)

Para obtener más información sobre los informes de análisis de formularios, consulte [Ver y comprender los informes de análisis de AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puede ver informes detallados y obtener más información sobre los clientes y sus interacciones con los formularios desde su cuenta de Analytics en Adobe Marketing Cloud.

#### Paso 3: Analizar los puntos de datos {#step-analyze-data-points}

En este paso, se analizarán los puntos de datos en el informe de análisis y se deducirá el rendimiento del formulario. Si no alcanza los KPI de éxito, elaborará hipótesis basadas en los datos y buscará posibles soluciones para resolver los problemas. Por ejemplo:

* Si el tiempo de rellenado promedio del formulario es mayor de lo esperado, es posible que este resulte complejo para los clientes, que no utilice terminologías estándar, que sea demasiado largo, etc. En ese caso, tal vez prefiera simplificar la estructura y los campos del formulario, rehacer el diseño, reducir la longitud o agregar descripciones de ayuda y ejemplos para los campos no estándares.
* Si los datos indican que la mayoría de los clientes acceden a la ayuda de uno de los paneles del formulario, es evidente que tienen dudas respecto a la información que deben rellenar. Puede que prefiera utilizar una terminología alternativa o agregar algunas entradas de ejemplo y una descripción de ayuda en ese panel.
* Si la tasa de anulación o abandono de un formulario es mayor de lo esperado, puede deberse a que tarda mucho tiempo en procesarse, a que los clientes acceden a él involuntariamente o a que es demasiado complicado. En ese caso, puede que desee optimizar la descripción del formulario que aparece en los resultados de búsqueda, simplificarlo, optimizarlo para que se cargue más rápido, etc.

Una vez que haya analizado estos puntos de datos y elaborado una hipótesis, realice los cambios necesarios en el formulario.

#### Paso 4: Validación del análisis y correcciones {#step-validate-your-analysis-and-fixes}

En este paso, validará los cambios realizados en el formulario y comprobará si afectan a la tasa de conversión.

**Ejecución de una prueba A/B**

La integración de AEM Forms con Target permite crear pruebas A/B para formularios adaptables. En las pruebas A/B, se presentan aleatoriamente a los clientes diferentes experiencias de un mismo formulario en tiempo real para saber cuál funciona mejor o genera un mayor número de conversiones. Una vez que haya obtenido datos significativos que indiquen que una experiencia ofrece una mejor conversión que la otra, puede declararla ganadora y, a partir de ese momento, utilizarla como la experiencia predeterminada visible para todos los clientes.

Para obtener más información sobre la creación de una prueba A/B para un formulario adaptable, consulte [Pruebas A/B para formularios adaptables](../../forms/using/ab-testing-adaptive-forms.md).

![Informe de resumen de ejemplo de la prueba A/B de un formulario adaptable](assets/ab-test-report-4.png)

## Prácticas recomendadas {#best-practices}

Las verdaderas prácticas recomendadas son las que identifica por sí mismo al realizar este flujo de trabajo. Se trata de prácticas exclusivas de su entorno y de sus requisitos. Obtenga conocimientos a través del flujo de trabajo y documéntelos como prácticas recomendadas.

A continuación, encontrará algunas recomendaciones sobre el diseño de formularios y la ejecución de pruebas A/B:

**Diseño de formularios**

* Cree formularios sencillos, breves y fácil de navegar. Utilice indicaciones direccionales para la navegación.
* Use terminologías estándares o comunes en los campos de formulario.
* Explique el campo y la entrada requerida mediante ejemplos o ayuda si hay algún aspecto que pueda resultar confuso para los usuarios.
* Valide las entradas de los usuarios a medida que escriben siempre que sea posible para evitar errores en el envío del formulario.
* Optimice los diseños para equipos de escritorio y dispositivos móviles.
* Rellene automáticamente información para usuarios conocidos.

**Pruebas A/B**

* Elabore una hipótesis e identifique las métricas de éxito antes de ejecutar la prueba A/B.
* Realice variaciones mínimas (preferiblemente de una en una) en la experiencia alternativa para saber qué ha influido en la tasa de conversión.
* Realice pruebas con frecuencia para eliminar las ineficiencias.
