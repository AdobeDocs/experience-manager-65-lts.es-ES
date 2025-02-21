---
title: Mejorar el rendimiento de los formularios grandes mediante la carga diferida
description: La carga diferida mejora significativamente el rendimiento de los formularios adaptables grandes y complejos al aplazar la inicialización y la carga de los fragmentos de formulario hasta que son visibles.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 91%

---

# Mejorar el rendimiento de los formularios grandes mediante la carga diferida{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/lazy-loading-adaptive-forms.html) |
| AEM 6.5 | Este artículo |

## Introducción a la carga diferida {#introduction-to-lazy-loading}

Cuando un formulario se vuelve grande y complejo e incluye cientos y miles de campos, los usuarios finales experimentan tiempos de respuesta largos cuando representan formularios en tiempo de ejecución. Para minimizar el tiempo de respuesta, los formularios adaptables permiten dividir cada formulario en fragmentos lógicos y configurarlo para retrasar la inicialización o la carga de los fragmentos hasta que el fragmento tenga que ser visible. Este proceso se denomina carga diferida. Además, los fragmentos configurados para la carga diferida se descargan una vez que el usuario se desplaza a otras secciones del formulario y los fragmentos ya no son visibles.

En primer lugar, vamos a explicar cuáles son los requisitos y los pasos preparatorios antes de configurar la carga diferida.

## Preparación para configurar la carga diferida {#preparing-to-configure-lazy-loading}

Antes de configurar la carga diferida de fragmentos en el formulario adaptable, es importante definir las estrategias para crear los fragmentos, identificar los valores que se utilizarán en los scripts o a los que se hará referencia en otros fragmentos y definir unas reglas para controlar la visibilidad de los campos en los fragmentos cargados de forma diferida.

* **Identificar y crear fragmentos**
Solo puede configurar fragmentos de formulario adaptable para la carga diferida. Un fragmento es un segmento independiente que reside fuera de un formulario adaptable y que puede reutilizarse en otros formularios. Por lo tanto, el primer paso para implementar la carga diferida es identificar las secciones lógicas de un formulario y convertirlas en fragmentos. Puede crear un fragmento desde cero o guardar un panel de formulario existente como fragmento.

  Para obtener más información sobre la creación de fragmentos, consulte [Fragmentos de formulario adaptables](../../forms/using/adaptive-form-fragments.md).

* **Identificar y marcar los valores globales**
Las transacciones basadas en Forms implican elementos dinámicos para capturar datos relevantes de los usuarios y procesarlos para simplificar la experiencia de rellenado de los formularios. Por ejemplo, el formulario tiene el campo A en el fragmento X, cuyo valor determina la validez del campo B en otro fragmento. En este caso, si el fragmento X está marcado para la carga diferida, el valor del campo A debe estar disponible para validar el campo B incluso cuando el fragmento X no está cargado. Para conseguirlo, puede marcar el campo A como global, lo que garantiza que su valor esté disponible para validar el campo B cuando el fragmento X no está cargado.

  Para obtener información sobre cómo convertir un valor de campo en global, consulte [Configuración de la carga diferida](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Escribir reglas para controlar la visibilidad de los campos**
Los formularios incluyen algunos campos y secciones que no son aplicables a todos los usuarios y en todas las condiciones. Los autores y desarrolladores de formularios utilizan la visibilidad o las reglas de Mostrar u ocultar para controlar su visibilidad en función de las entradas del usuario. Por ejemplo, el campo Dirección de la oficina no se muestra a los usuarios que eligen Desempleado en el campo Situación laboral en un formulario. Para obtener más información sobre cómo escribir reglas, consulte [Uso del Editor de reglas](../../forms/using/rule-editor.md).

  Puede utilizar reglas de visibilidad en los fragmentos cargados de forma diferida, de forma que los campos condicionales se muestren solo cuando sean necesarios. Además, puede marcar el campo condicional como global para hacer referencia a él en la expresión de visibilidad del fragmento cargado de forma diferida.

## Configuración de la carga diferida {#configuring-lazy-loading}

Realice los siguientes pasos para habilitar la carga diferida en un fragmento de formulario adaptable:

1. Abra el formulario adaptable que contiene el fragmento en el que desea habilitar la carga diferida en el modo Autor.
1. Seleccione el fragmento de formulario adaptable y seleccione ![cmppr](assets/cmppr.png).
1. En la barra lateral, habilita la opción **[!UICONTROL Cargar fragmento de forma diferida]** y selecciona **Listo**.

   ![Habilitar la carga diferida en el fragmento de formulario adaptable](assets/lazy-loading-fragment.png)

   Ahora la carga diferida está habilitada en el fragmento.

Puede marcar los valores de los objetos del fragmento cargado de forma diferida como globales, de modo que estén disponibles para su uso en scripts cuando el fragmento que los contiene no esté cargado. Haga lo siguiente:

1. Abra el fragmento del formulario adaptable en el modo Autor.
1. Seleccione el campo cuyo valor desee marcar como global y, a continuación, seleccione ![cmppr](assets/cmppr.png).
1. En la barra lateral, habilite la opción **Utilizar valor durante la carga diferida**.

   ![Campo de carga diferida en la barra lateral](assets/enable-lazy-loading.png)

   Ahora el valor está marcado como global y está disponible para su uso en scripts incluso cuando el fragmento que lo contiene aún no se ha cargado.

## Consideraciones y prácticas recomendadas para configurar la carga diferida {#considerations-and-best-practices-for-configuring-lazy-loading}

A continuación encontrará algunas limitaciones, recomendaciones y puntos importantes a tener en cuenta a la hora de trabajar con la carga diferida:

* Utilice formularios adaptables basados en esquemas XSD sobre formularios adaptables basados en XFA para configurar la carga diferida en formularios grandes. La mejora del rendimiento obtenida mediante la implementación de la carga diferida en los formularios adaptables basados en XFA es relativamente menor que la obtenida en los formularios adaptables basados en XSD.
* No configure la carga diferida en fragmentos de un formulario adaptable que utilicen el diseño **[!UICONTROL Adaptable: todo en una página sin navegación]** en el panel raíz. La configuración de diseño Adaptable provoca que todos los fragmentos se carguen simultáneamente en un formulario adaptable. También puede provocar una reducción del rendimiento.
* Se recomienda no configurar la carga diferida en el primer fragmento de un formulario adaptable.
* Se recomienda no configurar la carga diferida de los fragmentos del primer panel que se representa al cargar el formulario adaptable.
* La carga diferida es compatible con hasta dos niveles de la jerarquía de fragmentos.
* Asegúrese de que los campos marcados como globales sean únicos en cada formulario adaptable.
* Considere la posibilidad de escribir reglas de visibilidad para aquellos fragmentos que deban mostrarse u ocultarse según una condición. Por ejemplo, puede mostrar u ocultar el fragmento Datos del cónyuge en función del estado civil especificado por el usuario.
* Los componentes Archivo adjunto y Términos y condiciones no son compatibles con los fragmentos cargados de forma diferida.

### Prácticas recomendadas de scripts para configurar la carga diferida {#scripting-best-practices-for-configuring-lazy-loading}

Estos son algunos puntos importantes que debe tener en cuenta al desarrollar scripts para paneles de carga diferida:

* Asegúrese de que los scripts de inicialización y cálculo utilizados en los campos de un fragmento cargado de forma diferida son idempotentes. Los scripts idempotentes son aquellos que tienen el mismo efecto incluso después de varias ejecuciones.
* Utilice la propiedad de los campos disponible de forma global para que el valor de los campos de un panel de carga diferida esté disponible en el resto de los paneles de un formulario.
* No reenvíe el valor de referencia de un campo dentro de un panel de carga diferida, independientemente de si el campo está marcado como global en los fragmentos o no.
* Utilice la función Restablecer del panel para restablecer todos sus elementos visibles mediante la siguiente expresión de clic.\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;})).resetData()
