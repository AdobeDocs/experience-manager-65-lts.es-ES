---
title: 'Prácticas recomendadas para usar formularios adaptables '
description: Explica las prácticas recomendadas para configurar un proyecto de AEM Forms, desarrollar formularios adaptables y optimizar el rendimiento del sistema AEM Forms.
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: b87629fa-85a9-4024-963a-4761bc093e62
source-git-commit: d0529c8bce32e192cbbc7686f14825df57762363
workflow-type: tm+mt
source-wordcount: '5535'
ht-degree: 77%

---

# Prácticas recomendadas para usar formularios adaptables  {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/introduction) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Información general {#overview}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales simples y atractivas. Pero implementar, construir, ejecutar y mantener un ecosistema de AEM Forms eficiente y productivo requiere un esfuerzo concertado.

Este documento proporciona directrices y recomendaciones de las que pueden beneficiarse el administrador de formularios, los autores y los desarrolladores al trabajar con AEM Forms, especialmente con el componente de formularios adaptables. Se tratan las prácticas recomendadas, desde la configuración de un proyecto de desarrollo de formularios hasta la configuración, personalización, creación y optimización de AEM Forms. Estas prácticas recomendadas contribuyen colectivamente al rendimiento general del ecosistema de AEM Forms.

Además, estas son algunas lecturas recomendadas para prácticas recomendadas generales de AEM:

* [Prácticas recomendadas: Implementar y mantener AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas: Crear contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas: Administrar AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas: Desarrollar soluciones](/help/sites-developing/best-practices.md)

## Configurar AEM Forms {#set-up-and-configure-aem-forms}

### Configurar el proyecto de desarrollo de formularios {#setting-up-forms-development-project}

Una estructura de proyecto simplificada y estandarizada puede reducir considerablemente los esfuerzos de desarrollo y mantenimiento. Apache Maven es una herramienta de código abierto recomendada para la creación de proyectos de AEM.

* Usar Apache Maven `aem-project-archetype` para crear y administrar la estructura de proyectos de AEM. Crea plantillas y estructura recomendadas para el proyecto de AEM. Además, automatiza el procesamiento y cambia los sistemas de control para ayudar a administrar el proyecto.

   * Utilice el comando de maven `archetype:generate` para generar la estructura inicial.
   * Use el comando de maven `eclipse:eclipse` para generar los archivos del proyecto de Eclipse e importar el proyecto en Eclipse.

Para obtener más información, consulte [Cómo crear proyectos de AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

* La herramienta FileVault o VLT le ayuda a asignar el contenido de una instancia CRX o AEM a su sistema de archivos. Proporciona operaciones de administración del control de cambios, como el registro y la salida del contenido del proyecto de AEM. Consulte [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md).

* Si utiliza el entorno de desarrollo integrado en Eclipse, puede utilizar herramientas de desarrollo de AEM para la integración perfecta de Eclipse IDE con instancias de AEM para crear aplicaciones de AEM. Para obtener más información, consulte [Herramientas para desarrolladores de AEM para Eclipse](/help/sites-developing/aem-eclipse.md).

* No almacene ningún contenido ni realice ninguna modificación en la carpeta /libs. Cree superposiciones en carpetas /app para ampliar o sobrescribir las funcionalidades predeterminadas.

* Cuando cree paquetes para mover contenido, asegúrese de que las rutas de filtro de paquetes sean correctas y solo se mencionen las rutas requeridas.

* No almacene ningún contenido ni realice ninguna modificación en la carpeta /libs. Cree superposiciones en carpetas /app para ampliar o sobrescribir las funcionalidades predeterminadas.

* Defina las dependencias correctas para que los paquetes obliguen mantener un orden o una secuencia de instalación predeterminados.

* No cree ningún nodo referenciable en /libs o /apps.

### Planificar el entorno de creación {#planning-for-authoring-environment}

Una vez configurado el proyecto de AEM, defina una estrategia para crear y personalizar plantillas y componentes de formularios adaptables.

* Una plantilla de formulario adaptable es una página de AEM especializada que define la estructura y la información del encabezado y pie de página de un formulario adaptable. Una plantilla tiene diseños, estilos y estructuras básicos preconfigurados para un formulario adaptable. AEM Forms proporciona plantillas y componentes integrados que puede utilizar para crear formularios adaptables. Sin embargo, puede crear plantillas y componentes personalizados según sus necesidades. Se recomienda recopilar los requisitos para plantillas y componentes adicionales que necesite en los formularios adaptables. Para obtener más información, consulte [Personalizar formularios y componentes adaptables](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* Se recomienda cargar los paquetes de formularios mediante la interfaz de usuario de Form Manager en lugar de la interfaz de usuario de CRX Package Manager, ya que la carga de paquetes mediante CRX Package Manager a veces puede provocar anomalías.
* AEM Forms permite crear formularios adaptables basados en los siguientes modelos de formulario. Los modelos de formulario actúan como interfaz para el intercambio de datos entre un formulario y el sistema de AEM y proporcionan una estructura basada en XML para el flujo de datos dentro y fuera de un formulario adaptable. Además, los modelos de formulario imponen reglas y restricciones en los formularios adaptables en forma de restricciones de esquema y XFA.

   * **Ninguno**: los formularios adaptables creados con esta opción no utilizan ningún modelo de formulario. El XML de datos generado a partir de estos formularios tiene una estructura plana con campos y valores correspondientes.
   * **Esquema XML o JSON**: los esquemas XML y JSON representan la estructura en la que el sistema back-end de su organización produce o consume los datos. Puede asociar el esquema a un formulario adaptable y utilizar sus elementos para agregarle contenido dinámico. Los elementos del esquema están disponibles en la pestaña Objeto del modelo de datos del explorador de contenidos para crear formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.
   * **Plantilla de formulario XFA**: es un modelo de formulario ideal si tiene inversiones en formularios HTML5 basados en XFA. Proporciona una forma directa de convertir los formularios basados en XFA en formularios adaptables. Cualquier regla XFA existente se conservará en el formulario adaptable asociado. El formulario adaptable resultante admitirá construcciones XFA, como validaciones, eventos, propiedades y patrones.
   * **Modelo de datos de formulario**: es un modelo de formulario preferido si desea integrar sistemas backend como bases de datos, servicios web y perfiles de usuario de AEM para rellenar previamente formularios adaptables y escribir datos de formulario enviados de nuevo en los sistemas backend. Un editor del Modelo de datos de formulario permite definir y configurar entidades y servicios en un modelo de datos de formulario que se puede utilizar para crear formularios adaptables. Para obtener más información, consulte [Integración de datos de AEM Forms](/help/forms/using/data-integration.md).

Es importante elegir cuidadosamente el modelo de datos que no solo se adapte a sus necesidades, sino que amplíe sus inversiones existentes en recursos XFA y XSD, si las hay. Utilice el modelo XSD para crear plantillas de formulario porque el XML generado contiene datos según el XPATH definido por el esquema. El uso del modelo XSD como opción predeterminada para el modelo de datos de formulario también es útil porque desvincula el diseño de formulario del sistema backend que procesa y consume datos y mejora el rendimiento del formulario debido a que se asigna de uno a uno el campo de formulario. Además, el BindRef del campo puede convertirse en el XPATH de su valor de datos en XML.

Para obtener más información, consulte [Crear un formulario adaptable](/help/forms/using/creating-adaptive-form.md).

* Hay algunas secciones comunes en los formularios adaptables. Puede identificarlos y definir una estrategia para promover la reutilización del contenido. Los formularios adaptables permiten crear fragmentos independientes y reutilizarlos en todos los formularios. También puede guardar un panel en un formulario adaptable como un fragmento. Cualquier cambio en un fragmento se reflejará en todos los formularios asociados. Ayuda a reducir el tiempo de creación y garantiza la coherencia en todos los formularios. Además, el uso de fragmentos hace que los formularios adaptables sean ligeros, lo que mejora la experiencia de creación, especialmente de formularios grandes. Para obtener más información, consulte [Fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md).

### Personalizar formularios y componentes adaptables {#customize-components}

* AEM Forms proporciona plantillas de formulario adaptables integradas que puede utilizar para crear formularios adaptables. También puede crear sus propias plantillas. AEM proporciona plantillas estáticas y editables.

   * Los desarrolladores definen y configuran las plantillas estáticas.
   * Los autores crean plantillas editables mediante el editor de plantillas. El editor de plantillas permite definir una estructura básica y contenido inicial en una plantilla. Cualquier modificación en la capa de estructura se reflejará en todos los formularios que utilicen esa plantilla. El contenido inicial puede incluir una temática preconfigurada, un servicio de relleno previo, una acción de envío, etc. Sin embargo, esta configuración se puede modificar para un formulario con el editor de formularios. Para obtener más información, consulte [Plantillas de formulario adaptables](/help/forms/using/template-editor.md).

* Para diseñar un campo o una instancia de panel específicos, utilice [estilo dentro de la línea](/help/forms/using/inline-style-adaptive-forms.md). Como alternativa, puede definir una clase en un archivo CSS y especificar su nombre en la propiedad Clase CSS del componente.
* Incluya una biblioteca de cliente en un componente para aplicar estilos de forma coherente en todos los formularios adaptables o fragmentos que utilicen ese componente. Para obtener más información, consulte [Crear un componente de página de formulario adaptable](/help/forms/using/custom-adaptive-forms-templates.md).
* Aplique estilos definidos en una biblioteca de cliente para seleccionar formularios adaptables, para hacerlo, especifique la ruta a la biblioteca de cliente en el campo de ruta del archivo CSS en las propiedades del contenedor de formularios adaptables.
* Para crear una biblioteca de cliente con sus estilos, puede configurar el archivo CSS personalizado en la base del Editor de temáticas clientlib o en las propiedades del contenedor de formularios.
* Los formularios adaptables proporcionan diseños de panel, como capacidad de respuesta, pestañas, acordeones y asistente, para controlar cómo se distribuyen los componentes de formulario en un panel. Puede crear diseños de panel personalizados y ponerlos a disposición de los autores de formularios para utilizarlos. Para obtener más información, consulte [Crear componentes de diseño personalizados para formularios adaptables](/help/forms/using/custom-layout-components-forms.md).
* También puede personalizar componentes de formulario adaptables específicos, como campos y diseño de panel.

   * Utilice la funcionalidad de AEM [Superposición](/help/sites-developing/overlays.md) para modificar una copia de un componente. No se recomienda modificar los componentes predeterminados.
   * Para personalizar el diseño de los componentes de formulario adaptables listos para usar en /libs, [cree componentes de diseño personalizados](/help/forms/using/custom-layout-components-forms.md) además de [diseños predeterminados](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduzca interactividades personalizadas mediante la creación de widgets o apariciones personalizados. No se recomienda modificar los componentes predeterminados. Para obtener más información, consulte [Marco de trabajo de aspecto](/help/forms/using/introduction-widgets.md).

* Consulte [Administrar información personal](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) para recomendaciones sobre la administración de datos PII.

### Crear plantillas de formulario

Puede crear un formulario adaptable con las plantillas de formulario habilitadas en **Explorador de configuración**. Para habilitar las plantillas de formulario, consulte [Crear una plantilla de formulario adaptable](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template).

Las plantillas de formulario también se pueden cargar desde paquetes de formularios adaptables creados en otro equipo de creación. Las plantillas de formulario están disponibles mediante al instalar [paquetes aemforms-references-*](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases). Algunas de las prácticas recomendadas son las siguientes:

* El modo de ejecución **nosamplecontent** solo se recomienda para el autor y no para los nodos de publicación.
* La creación de recursos, como formularios adaptables, temáticas, plantillas o configuraciones de nube, se realiza solo sobre nodos de autor, que se pueden publicar en los nodos configurados de publicación.
Para obtener más información, consulte [Publicar y cancelar la publicación de formularios y documentos](/help/forms/using/publishing-unpublishing-forms.md)
* El paquete de complementos de Forms es necesario para que la creación y la publicación admitan las operaciones del servicio de documentos; por lo tanto, puede considerarse como una dependencia.
Si solo desea plantillas de muestra, temáticas y paquetes de DOR relacionados con Forms, puede descargarlos desde [paquetes aemforms-references-*](/help/forms/using/upgrade-forms-osgi.md).

Para obtener más información, consulte las prácticas recomendadas en [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

## Crear formularios adaptables {#author-adaptive-forms}

### Usar la interfaz de usuario táctil para la creación {#using-touch-optimized-ui-for-authoring}

* Utilice el explorador de objetos de la barra lateral para acceder rápidamente a los campos situados en la parte inferior de la jerarquía del formulario. Puede utilizar el cuadro de búsqueda para buscar objetos en el árbol de objetos o formularios y navegar de un objeto a otro.
* Para ver y editar las propiedades de un componente en el explorador de componentes de la barra lateral, seleccione el componente y haga clic en ![cmppr-1](assets/cmppr-1.png). También puede hacer doble clic en un componente para ver sus propiedades en el explorador de propiedades.
* Utilice los métodos abreviados del teclado para realizar acciones rápidas en los formularios. Consulte [Atajos de teclado de AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Se recomiendan los componentes de formulario adaptables para utilizarlos únicamente en páginas de formulario adaptables. Los componentes dependen de su jerarquía principal. Por lo tanto, no los utilice en una página de AEM.

Consulte también las descripciones de los componentes y las prácticas recomendadas en [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

### Usar reglas en formularios adaptables {#using-rules-in-adaptive-forms}

AEM Forms proporciona un [editor de reglas](/help/forms/using/rule-editor.md) que le permite crear reglas para agregar un comportamiento dinámico a los componentes del formulario adaptable. Con estas reglas, se pueden evaluar condiciones y acciones del activador en componentes como mostrar u ocultar campos, calcular valores, cambiar listas desplegables de forma dinámica, etc.

El editor de reglas proporciona un editor visual y un editor de código para escribir reglas. Tenga en cuenta lo siguiente al escribir reglas mediante el modo de editor de código:

* Utilice nombres significativos y únicos para los campos y componentes de formulario para evitar posibles conflictos al escribir reglas.
* Use el operador `this` para que un componente se haga referencia a sí mismo en una expresión de regla. Garantiza que la regla será válida incluso si cambia el nombre del componente. Por ejemplo, `field1.valueCommit script: this.value > 10`.

* Utilice nombres de componentes cuando haga referencia a otros componentes del formulario. Utilice la propiedad `value` para recuperar el valor de un campo o componente. Por ejemplo, `field1.value`.

* Consulte los componentes por jerarquía única relativa para evitar conflictos. Por ejemplo, `parentName.fieldName`.

* Cuando administre reglas complejas o comúnmente utilizadas, considere la posibilidad de escribir lógica empresarial como funciones en una biblioteca de cliente independiente que puede especificar y reutilizar en formularios adaptables. La biblioteca de cliente debe ser una biblioteca independiente y no debe tener dependencias externas, excepto jQuery y Underscore.js. También puede utilizar la biblioteca de cliente para aplicar [revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) de los datos de formulario enviados.
* Los formularios adaptables proporcionan un conjunto de API que puede utilizar para comunicarse con los formularios adaptables y realizar acciones en ellos. Algunas de las API clave son las siguientes: Para obtener más información, consulte [Referencia de la API de la biblioteca JavaScript para formularios adaptables](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions).

   * `guideBridge.reset()`: restablece un formulario.
   * `guideBridge.submit()`: envía un formulario.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: define el enfoque en un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: valida un formulario.
   * `guideBridge.getDataXML(options)`: obtiene los datos del formulario como XML.
   * `guideBridge.resolveNode(somExpression)`: obtiene un objeto de formulario.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: define la propiedad de un objeto de formulario.
   * Además, puede utilizar las siguientes propiedades de campo:

      * `field.value` para cambiar el valor de un campo.
      * `field.enabled` para habilitar o deshabilitar un campo.
      * `field.visible` para cambiar la visibilidad de un campo.

* Es posible que los autores de formularios adaptables tengan que escribir código JavaScript para crear lógica empresarial en un formulario. Aunque JavaScript es potente y eficaz, es probable que pueda comprometer las expectativas de seguridad. Por lo tanto, debe asegurarse de que el autor del formulario sea una persona de confianza y de que haya procesos para revisar y aprobar el código JavaScript antes de que se ponga en producción un formulario. El administrador puede restringir el acceso al editor de reglas a los grupos de usuarios en base a su rol o función. Consulte [Conceder acceso al Editor de reglas a determinados grupos de usuarios.](/help/forms/using/rule-editor-access-user-groups.md).
* Puede utilizar expresiones en reglas para hacer dinámicos los formularios adaptables. Todas las expresiones son expresiones JavaScript válidas y utilizan API de modelos de scripts de formularios adaptables. Estas expresiones devuelven valores de ciertos tipos. Para obtener más información sobre las expresiones y las prácticas recomendadas que las rodean, consulte [Expresiones de formulario adaptables](/help/forms/using/adaptive-form-expressions.md).

* Adobe recomienda utilizar las operaciones sincrónicas de JavaScript sobre las asincrónicas al crear reglas con el editor de reglas. Se desaconseja el uso de operaciones asincrónicas. Sin embargo, si se encuentra en una situación en la que las operaciones asincrónicas son inevitables, es esencial implementar las funciones de Cierre de JavaScript. Al hacerlo, puede proteger de forma eficaz contra cualquier posible condición de carrera, lo que garantiza que las implementaciones de reglas ofrezcan un rendimiento óptimo y mantengan la estabilidad en todo.

  Por ejemplo, supongamos que necesitamos recuperar datos de una API externa y luego aplicar algunas reglas basadas en esos datos. Utilizamos un cierre para gestionar la llamada asincrónica a la API y garantizar que las reglas se apliquen después de recuperar los datos. Este es un ejemplo de código:

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  En este ejemplo, `fetchDataFromAPI` simula una llamada de API asincrónica con `setTimeout`. Una vez recuperados los datos, invoca la función de llamada de retorno proporcionada, que es el cierre para administrar la aplicación de reglas posterior. La función `ruleImplementation` contiene la lógica de regla.


### Trabajar con temáticas {#working-with-themes}

La adaptación para las temáticas le permite crear estilos reutilizables que se pueden aplicar en todos los formularios para lograr un aspecto y un estilo coherentes. Utilice Temáticas para definir el estilo de los componentes y paneles del formulario. Algunas prácticas recomendadas relacionadas con los temáticas son las siguientes:

* Utilizar la biblioteca de recursos para aplicar rápidamente estilos de texto, fondo e imágenes. Cuando se agrega un estilo en la biblioteca de recursos, estará disponible para otras temáticas y para el modo de estilo de la interfaz de usuario del editor de formularios.
* Aplique la configuración global como fuente y fondo de página mediante el selector de nivel de página.
* Utilice bibliotecas de cliente para importar estilos existentes o avanzados en sus temáticas.
* Puede anular el estilo de campos, paneles o botones específicos de una capa de estilo de formulario.
* Si una temática no cumple los requisitos de estilo, puede utilizar clases predefinidas como guideFieldNode, guideFieldLabel, guideFieldWidget y guidePanelNode para aplicar un estilo común a todos los formularios.

Para obtener más información, consulte [Temáticas](/help/forms/using/themes.md).

### Optimizar el rendimiento de formularios grandes y complejos {#optimizing-performance-of-large-and-complex-forms}

Los autores de formularios y los usuarios finales suelen tener problemas de rendimiento al cargar formularios grandes en el modo de creación o durante la ejecución. A medida que aumenta el número de objetos (campos y paneles) en el formulario, la experiencia de creación y de ejecución comienza a degradarse. También evita que varios autores colaboren y creen un formulario simultáneamente.

Tenga en cuenta las siguientes prácticas recomendadas para superar los problemas de rendimiento con formularios grandes:

* Se recomienda crear formularios adaptables mediante el modelo de datos de formulario XSD incluso cuando sea posible convertir un XFA a un formulario adaptable.
* Incluir solo los campos y paneles en formularios adaptables que capturan información del usuario. Considere la posibilidad de mantener el contenido estático como mínimo o utilice direcciones URL para abrirlo en una ventana independiente.
* Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de los formularios. Por ejemplo: detalles personales, dirección, detalles de empleo, etc. Cree [fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md) para elementos y secciones de formulario comunes y utilícelos en todos los formularios. También puede guardar un panel en un formulario existente como un fragmento. Cualquier cambio en un fragmento se reflejará en todos los formularios adaptables asociados. Promueve la creación colaborativa, ya que varios autores pueden trabajar simultáneamente en diferentes fragmentos que conforman un formulario.

   * De forma similar a los formularios adaptables, se recomienda que todos los estilos específicos de fragmento y los scripts personalizados se definan en la biblioteca de cliente mediante el cuadro de diálogo contenedor de fragmentos. Además, intente crear fragmentos autosuficientes que no dependan de objetos externos.
   * Evite utilizar scripts entre fragmentos. Si hay algún objeto fuera del fragmento al que deba hacer referencia, intente que dicho objeto forme parte del formulario principal. Si el objeto debe residir en otro fragmento, refiérase a él por su nombre en el script.

* Utilice Guardar y reanudar con el guardado automático para guardar el formulario adaptable periódicamente y permitir que los usuarios vuelvan más tarde para completarlo.
* Configure los fragmentos para que se carguen de forma diferida. Durante el tiempo de ejecución, los fragmentos marcados para cargarse de forma diferida solo se representarán cuando sean necesarios. Reduce significativamente el tiempo de carga de los formularios grandes. También se admite en fragmentos con paneles repetibles. Para obtener más información, consulte [Configurar la carga diferida](/help/forms/using/lazy-loading-adaptive-forms.md).

   * No configure la carga diferida en fragmentos en un diseño de cuadrícula adaptable o en el primer panel.
   * Los componentes Archivo adjunto y Términos y condiciones no son compatibles con los fragmentos cargados de forma diferida.
   * Marque un valor en un panel cargado de forma diferida como Usar valor globalmente si ese valor se utiliza en alguna otra parte del formulario, de modo que el valor esté disponible para su uso cuando se descargue el panel que lo contiene.
   * Considere la posibilidad de escribir reglas de visibilidad para aquellos fragmentos que deban mostrarse u ocultarse según una condición.
* Establezca el valor del **Número de llamadas por solicitud** en el **Servlet principal de Apache Sling** a un número bastante grande. Permite al servidor de Forms permitir llamadas adicionales. La configuración muestra un valor predeterminado de 1500. El valor 1500 llamadas es para otros componentes de Experience Manager, como Sites y Recursos. El conjunto de valores predeterminado de los formularios adaptables es 20000. Si encuentra el error `too many calls` en los registros o si el formulario no se puede procesar, intente aumentar el valor a un número mayor para resolver el problema. Si el número de llamadas supera los 20 000, el formulario es complejo y puede tardar algún tiempo en procesarse en el explorador. Esto solo ocurrirá la primera vez que se cargue el formulario, después de que se almacene en la memoria caché. Una vez que el formulario se almacene en la memoria caché, el rendimiento no se verá afectado de forma significativa.

### Rellenado previo de formularios adaptables {#prefilling-adaptive-forms}

Puede rellenar previamente los campos de formulario adaptables con datos recuperados del servidor para ayudar a los usuarios a rellenar rápidamente el formulario y evitar errores de escritura.

* AEM Forms proporciona un servicio de rellenado previo para leer datos de un archivo XML de datos predefinido y rellenar previamente los campos de un formulario adaptable con el contenido del archivo XML.
* El XML con datos de rellenado previo debe ser compatible con el esquema del modelo de formulario asociado al formulario adaptable.
* Incluya`afBoundedData` y secciones `afUnBoundedData` en el XML de rellenado previo para rellenar previamente los campos enlazados y no enlazados en un formulario adaptable.

* Para los formularios adaptables basados en el modelo de datos de formulario, AEM Forms proporciona el servicio de rellenado previo del modelo de datos de formulario integrado. El servicio de relleno previo consulta las fuentes de datos de los objetos del modelo de datos en el formulario adaptable y rellena los valores de campo al procesar el formulario.
* También puede utilizar los protocolos de archivo, crx, servicio o http para rellenar previamente los formularios adaptables.
* AEM Forms admite servicios de relleno previo personalizados que se pueden insertar como servicio OSGi para rellenar previamente formularios adaptables.

Para obtener más información, consulte [Rellenar previamente campos de formulario adaptables](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firmar y enviar formularios adaptables {#signing-and-submitting-adaptive-forms}

Los formularios adaptables requieren enviar acciones para procesar los datos especificados por el usuario. Una acción de envío determina la tarea realizada en los datos enviados mediante un formulario adaptable.

* Hay varias acciones de envío disponibles de forma predeterminada en los formularios adaptables. Para obtener más información, consulte [Configurar la acción de envío](/help/forms/using/configuring-submit-actions.md).
* Puede escribir una acción de envío personalizada si las acciones de envío predeterminadas no cumplen con su caso de uso. Para obtener más información, consulte [Escribir una acción de envío personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md).
* Incluya validaciones del lado del servidor para evitar el envío de datos no válidos.

Puede utilizar la experiencia de varias firmas de Adobe Sign en los formularios adaptables. Tenga en cuenta lo siguiente al configurar Adobe Sign en formularios adaptables. Para obtener más información, consulte [Usar Adobe Sign en un formulario adaptable](/help/forms/using/working-with-adobe-sign.md).

* El formulario adaptable habilitado para Adobe Sign solo se envía después de que todos los firmantes hayan firmado el formulario. Forms aparecerá en estado de firma pendiente hasta que todos los firmantes firmen el formulario.
* Puede configurar la experiencia de firma en el formulario o redirigir a los firmantes a una página de firma en el envío.
* Configure la experiencia de firma secuencial o paralela, según corresponda.

### Generar documento de registro {#generating-document-of-record}

Un documento de registro (DoR) es una versión PDF aplanada de un formulario adaptable que se puede imprimir, firmar o archivar.

* Según el modelo de datos de formulario en el que se base un formulario adaptable, puede configurar una plantilla para el DoR de la siguiente manera:

   * **Plantilla de formulario XFA**: utilice el archivo XDP asociado como plantilla del DoR.
   * **Esquema XSD**: utilice la plantilla XFA asociada que utilice el mismo esquema XML utilizado por el formulario adaptable.
   * **Ninguno**: utilice el DoR generado automáticamente.

* Configure el encabezado, pie de página, imágenes, color, fuente, etc. a la derecha de la pestaña Documento de registro del editor de formularios adaptables.
* Use `DoRService` para generar el DoR mediante programación.
* Excluir los campos ocultos del documento de registro.
* Use el parámetro de solicitud `afAcceptLang` para ver el DoR en otra configuración regional.

### Depurar y probar formularios adaptables {#debugging-and-testing-adaptive-forms}

[El complemento AEM Chrome](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) es una extensión del explorador para Google Chrome que proporciona herramientas para depurar formularios adaptables. Los creadores y desarrolladores de formularios pueden utilizar estas herramientas para lo siguiente:

* Identificar cuellos de botella y optimizar el rendimiento del procesamiento del formulario
* Depurar palabras clave y errores bindRef en el formulario
* Habilitar y configurar registros
* Depurar reglas y scripts en el formulario
* Explorar y obtener más información sobre las API de guideBridge

Para obtener más información, consulte [Complemento AEM Chrome: formulario adaptable](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Validar formularios adaptables en el servidor de AEM {#validating-adaptive-forms-on-aem-server}

Las validaciones del lado del servidor son necesarias para evitar cualquier intento de omitir las validaciones en el cliente y cualquier posible compromiso de los envíos de datos y las violaciones de reglas comerciales. Las validaciones del lado del servidor se ejecutan en el servidor al cargar la biblioteca de cliente necesaria.

* Incluya funciones en una biblioteca de cliente para validar expresiones en formularios adaptables y especifique la biblioteca de cliente en el cuadro de diálogo del contenedor de formularios adaptables. Para obtener más información, consulte [Revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validación del lado del servidor valida el modelo de formulario. Se recomienda crear una biblioteca de cliente independiente para las validaciones y no mezclarla con otras cosas como el estilo del HTML y la manipulación DOM en la misma biblioteca de cliente.

### Localizar formularios adaptables {#localizing-adaptive-forms}

AEM proporciona flujos de trabajo de traducción que puede utilizar para localizar formularios adaptables. Para obtener más información, consulte [Usar flujo de trabajo de traducción de AEM para localizar formularios adaptables](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Algunas prácticas recomendadas al localizar formularios adaptables son las siguientes:

* Utilice fragmentos de formulario adaptables para elementos comunes en todos los formularios y localice fragmentos. Garantiza que localice un fragmento una vez y se refleje en todos los formularios en los que se utilice el fragmento localizado.
* Las modificaciones como agregar un componente nuevo o aplicar un script en un formulario localizado no se localizan automáticamente. Por lo tanto, debe finalizar un formulario antes de localizarlo para evitar varios ciclos de localización.
* Use el parámetro de solicitud`afAcceptLang` para anular la configuración regional del explorador y procesar el formulario en la configuración regional especificada. Por ejemplo, la siguiente URL es forzada a procesar el formulario en la configuración regional japonesa, independientemente de la configuración regional especificada en la configuración del explorador:

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms admite actualmente la localización del contenido de los formularios adaptables en las configuraciones regionales de Inglés (en), Español (es), Francés (fr), Italiano (it), Alemán (de), Japonés (ja), Portugués brasileño (pt-BR), Chino (zh-CN), Chino taiwanés (zh-TW) y Coreano (ko-KR). Sin embargo, se puede agregar compatibilidad con nuevas configuraciones regionales para formularios adaptables en el tiempo de ejecución. Para obtener más información, consulte [Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables](/help/forms/using/supporting-new-language-localization.md).

## Preparar un proyecto de formularios para producción {#prepare-forms-project-for-production}

### Agregar un servidor de procesamiento de formularios {#adding-forms-processing-server}

Puede configurar una instancia adicional del servidor de AEM Forms que reside detrás del firewall en una zona segura. Puede utilizar esta instancia para lo siguiente:

* **Procesamiento por lotes**: trabajos que son recurrentes o están programados en lotes con una carga pesada. Por ejemplo, imprimir instrucciones, generar correspondencias y utilizar servicios de documentos como el Generador de PDF, Salida y Assembler.
* **Almacenar datos PII**: guarde los datos PII en el servidor de procesamiento. No es obligatorio si ya utiliza un proveedor de almacenamiento personalizado para almacenar datos PII.

### Mover el proyecto a otro entorno {#moving-project-to-another-environment}

A menudo, debe mover los proyectos de AEM de un entorno a otro. Algunas de las cosas clave que hay que recordar al moverlos son las siguientes:

* Haga una copia de seguridad de las bibliotecas de cliente, del código personalizado y de las configuraciones existentes.
* Implemente paquetes de productos y parches manualmente y en el orden especificado en el entorno nuevo.
* Implemente paquetes de código específicos del proyecto y paquetes manualmente y como paquete independiente en el servidor de AEM nuevo.
* (*AEM Forms solo en JEE*) Implementar LCA y DSC manualmente en el servidor del flujo de trabajo de Forms.
* Use [Exportar-Importar](/help/forms/using/import-export-forms-templates.md) para mover recursos al entorno nuevo. También puede configurar el agente de replicación y publicar los recursos.
* Al actualizar, reemplace todas las API y características obsoletas con API y características nuevas.

### Configurar AEM {#configuring-aem}

Algunas prácticas recomendadas para configurar AEM para mejorar el rendimiento general son las siguientes:

* Habilitar la compresión de la biblioteca de cliente HTML para JavaScript y CSS desde la consola Felix.
* Almacenar en la memoria caché todas las bibliotecas de cliente en `/etc.clientlibs/fd` y cualquier biblioteca de cliente personalizada adicional en AEM Dispatcher para aumentar la capacidad de respuesta y seguridad de los formularios publicados. Para obtener más información, consulte [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher.html).

* No almacenar en la memoria caché `/content/forms/af/` y rutas`/content/dam/formsanddocuments/*`. para obtener información detallada sobre la configuración del almacenamiento en la memoria caché de formularios adaptables, consulte [Almacenamiento en la memoria caché de formularios adaptables](/help/forms/using/configure-adaptive-forms-cache.md).

* Habilitar el HTML mediante el módulo de compresión del servidor web. Para obtener más información, consulte [Ajustar el rendimiento del servidor de AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumentar las llamadas por configuración de solicitud para formularios grandes. Consulte [Optimizar el rendimiento de formularios grandes y complejos](#optimizing-performance-of-large-and-complex-forms).
* Crear [páginas de error personalizadas mostradas por el administrador de errores](/help/sites-developing/customizing-errorhandler-pages.md).
* Asegurar el servidor de AEM Forms.

   * Usar el modo de ejecución `nosamplecontent` para asegurarse de que no haya contenido ni usuarios de muestra implementados en el servidor de producción. Consultar [Ejecutar AEM en el modo Producción lista](/help/sites-administering/production-ready.md).

* Mantener el tamaño de la pila a un mínimo de 8 GB. Para otras configuraciones, consulte [Ajustar el rendimiento del servidor de AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilice sesiones de usuario de servicio en lugar de sesiones de administración para ejecutar tareas de nivel de servicio. Para obtener más información, consulte [Autenticar el servicio](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/es/)

### Configurar el almacenamiento externo para borradores y datos de formularios enviados {#external-storage}

En un entorno de producción, se recomienda no almacenar datos de formularios enviados en el repositorio de AEM. La implementación predeterminada de Forms Portal Store, Store Content y Store PDF envía acciones y almacena datos de formulario en el repositorio de AEM. Estas acciones de envío solo están pensadas para fines de demostración. Además, las funciones Guardar y reanudar y Guardar automáticamente utilizan el almacenamiento del portal de forma predeterminada. Por lo tanto, considere las siguientes recomendaciones:

* **Almacenar datos de borrador**: si utiliza la función Borrador de los formularios adaptables, debe implementar una interfaz de proveedor de servicios (SPI) personalizada para almacenar los datos en modo de borrador en un almacenamiento más seguro, como la base de datos. Para obtener más información, consulte [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

* **Almacenar datos de envío**: si utiliza el repositorio de envío del portal de formularios, debe implementar un SPI personalizado para almacenar los datos de envío en una base de datos. Consulte [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md) para una integración de ejemplo.

  También puede escribir una acción de envío personalizada que almacene datos de formulario y los datos adjuntos en un almacenamiento seguro. Consulte [Escribir una acción de envío personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md) para obtener más información.

* **Longitud del ID del borrador**: al guardar un formulario adaptable como borrador, se genera un ID de borrador para identificar el borrador de forma exclusiva. El valor mínimo de la longitud del campo de ID de borrador es de 26 caracteres. Adobe recomienda establecer la longitud de ID de borrador en 26 caracteres o más.

### Administrar información personal identificable {#handling-personally-identifiable-information}

Uno de los desafíos clave para las organizaciones es cómo manejar los datos de identificación personal (PII). A continuación se indican algunas prácticas recomendadas que le ayudarán a administrar estos datos:

* Utilizar un almacenamiento externo seguro como la base de datos para almacenar datos de formularios enviados y en modo de borrador. Consulte [Configurar el almacenamiento externo para datos de formularios enviados y en modo de borrador](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilice el componente de formulario Términos y condiciones para obtener el consentimiento explícito del usuario antes de activar el guardado automático. En este caso, habilite el guardado automático solo cuando el usuario acepte las condiciones del componente Términos y condiciones.

## Elija el Editor de reglas, el Editor de código o las Bibliotecas de cliente personalizadas para su formulario adaptable {#RuleEditor-CodeEditor-ClientLibs}

### Editor de reglas {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

El Editor de reglas de AEM Forms proporciona una interfaz visual para crear y administrar reglas, lo que reduce la necesidad de utilizar una programación extensa. Puede resultar especialmente útil para usuarios empresariales o diseñadores de formularios que pueden no tener habilidades de programación avanzadas, pero necesitan definir y mantener reglas empresariales dentro de los formularios. Aquí analizamos algunos casos de uso en los que el editor de reglas le permite:

* <!-- Allows you --> Definir reglas empresariales para los formularios sin necesidad de una programación extensa.
* <!-- Use the Rule Editor when you need --> Implementar la lógica condicional en los formularios. Esto incluye mostrar u ocultar elementos de formulario, modificar valores de campo basados en determinadas condiciones o cambiar dinámicamente el comportamiento de los formularios.
* <!--When you want --> Para aplicar reglas de validación de datos en los envíos de formularios, se puede utilizar el Editor de reglas para definir las condiciones de validación.
* <!-- When you need --> Para integrar los formularios con fuentes de datos externas (FDM) o servicios de, el Editor de reglas puede ayudar a definir reglas para recuperar, mostrar o manipular datos durante las interacciones de formularios.
* <!-- If you want -->Para crear formularios dinámicos e interactivos que respondan a las acciones del usuario, el Editor de reglas permite definir reglas que rigen el comportamiento de los elementos del formulario en tiempo real.

El editor de reglas está disponible tanto para componentes de AEM Forms Foundation como para componentes principales.

### Editor de código {#code-editor}

El Editor de código es una herramienta dentro de Adobe Experience Manager (AEM) Forms que le permite escribir scripts personalizados y código para una funcionalidad más compleja y avanzada en los formularios. Aquí analizamos algunos casos de uso:

* Cuando necesite implementar una lógica personalizada del lado del cliente o un comportamiento que vaya más allá de las capacidades del Editor de reglas de AEM Forms. El Editor de código le permite escribir código JavaScript para controlar interacciones, cálculos o validaciones complejos.
* Si el formulario requiere procesamiento en el servidor o integración con sistemas externos, puede utilizar el Editor de código para escribir scripts personalizados en el servidor. Puede acceder a la API de guideBridge en el editor de código para implementar cualquier lógica compleja en eventos y objetos de formulario.
* Cuando se requieren interfaces de usuario altamente personalizadas que vayan más allá de las capacidades estándar de los componentes de AEM Forms, el Editor de código permite implementar estilos y comportamientos personalizados, o incluso crear componentes de formulario personalizados.
* Si el formulario implica operaciones asincrónicas como la carga asincrónica de datos, puede utilizar el Editor de código para administrar estas operaciones mediante código JavaScript asincrónico personalizado.

Es importante tener en cuenta que el uso del Editor de código requiere una buena comprensión de la arquitectura de JavaScript y AEM Forms. Además, al implementar el código personalizado, asegúrese de seguir las prácticas recomendadas, cumplir las directrices de seguridad y probar el código a fondo para evitar posibles problemas en entornos de producción. Puede implementar una llamada de retorno para FDM mediante el editor de código.

El editor de código solo está disponible para el componente AEM Forms Foundation. Para los componentes principales de un formulario adaptable, puede utilizar funciones personalizadas para crear sus propias reglas de formulario, que se describen en la siguiente sección.

### Funciones personalizadas {#custom-client-libs}

El uso de bibliotecas de cliente personalizadas en AEM Forms (Adobe Experience Manager Forms) puede resultar beneficioso en varios casos para mejorar la funcionalidad, el estilo o el comportamiento de los formularios. Estas son algunas situaciones en las que el uso de bibliotecas de cliente personalizadas podría ser adecuado:

* Si necesita implementar un diseño o una personalización de marca únicos para los formularios que vayan más allá de las capacidades de las opciones de estilo predeterminadas que proporciona AEM Forms, puede optar por crear bibliotecas de cliente personalizadas para controlar la apariencia.
* Si necesita lógica personalizada del lado del cliente, reutilización de métodos en varios formularios o comportamientos que no se pueden lograr con las funciones estándar de AEM Forms. Esto puede incluir interacciones de formularios dinámicos, validación personalizada o integración con bibliotecas de terceros.
* Para mejorar el rendimiento de los formularios optimizando y minimizando los recursos del lado del cliente. Las bibliotecas de cliente personalizadas se pueden utilizar para empaquetar y comprimir archivos JavaScript y CSS, lo que reduce el tiempo total de carga de la página.
* Cuando necesite integrar bibliotecas o marcos de JavaScript adicionales que no estén incluidos en la configuración predeterminada de AEM Forms. Esto puede ser necesario para funciones como selectores de fechas mejorados, gráficos u otros componentes interactivos.

Antes de decidir utilizar bibliotecas de cliente personalizadas, es importante tener en cuenta la sobrecarga de mantenimiento, los posibles conflictos con futuras actualizaciones y el cumplimiento de las prácticas recomendadas. Asegúrese de que las personalizaciones estén bien documentadas y probadas para evitar problemas durante las actualizaciones o al colaborar con otros desarrolladores.

>[!NOTE]
> La función personalizada está disponible tanto para componentes principales como para componentes de base de AEM Forms.

**Ventajas de las funciones personalizadas:**

**Funciones personalizadas** proporcionan una ventaja notable sobre el **Editor de código** porque proporciona una clara separación entre contenido y código, lo que mejora la colaboración y optimiza los flujos de trabajo. Se recomienda utilizar funciones personalizadas para las siguientes ventajas:

* **Use sin problemas el control de versiones como Git:**
   * El aislamiento del código del contenido reduce significativamente los conflictos de Git durante la administración de contenido y promueve un repositorio bien organizado.
   * Funciones personalizadas es útil para proyectos con varios colaboradores que trabajan simultáneamente.

* **Beneficios técnicos:**
   * Las funciones personalizadas ofrecen modularidad y encapsulación.
   * Los módulos se pueden desarrollar, probar y mantener de forma independiente.
   * Mejora la reutilización y el mantenimiento del código.

* **Proceso de desarrollo eficiente:**
   * La modularidad permite a los desarrolladores centrarse en funcionalidades específicas.
   * Reduce la carga de los desarrolladores al reducir las complejidades de todo el código base para un proceso de desarrollo más eficiente.
