---
title: Introducción a la secuencia de formulario de varios pasos
description: Con AEM Forms, puede definir la secuencia de paneles de formulario en la que desea que los usuarios naveguen y rellenen un formulario adaptable.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 57%

---

# Introducción a la secuencia de formulario de varios pasos{#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. En este artículo se describe un método antiguo para crear Forms adaptable mediante componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | Este artículo |


Los formularios adaptables permiten a los autores de formularios crear una experiencia de captura de datos de varios pasos con gran facilidad. Estos formularios incluyen compatibilidad para crear varios paneles y asociar cada uno con diferentes patrones de navegación. Los autores de formularios pueden agrupar los campos de formulario en secciones lógicas y representar un grupo como un panel. La navegación general entre los paneles se controla mediante el diseño del panel. Los autores pueden elegir organizar los paneles en diferentes diseños, por ejemplo, colocándolos secuencialmente utilizando el diseño Asistente o de forma ad hoc utilizando el diseño con pestañas. Para obtener información sobre los diseños de panel, consulte [Funciones de diseño de formularios adaptables](../../forms/using/layout-capabilities-adaptive-forms.md).

Normalmente, durante la experiencia de cumplimentación de formularios, hay que seguir más pasos además de capturar los datos. Un envío de formulario completo puede incluir otros pasos, como firmar el formulario de forma digital, comprobar la información rellenada en el formulario y procesar pagos. Cada caso es diferente.

Si su caso de uso requiere seguir un conjunto de pasos para la captura de datos o hay algún reglamento que exige que se sigan unos pasos específicos, AEM Forms proporciona una forma de aplicar esa estructura común a todos los formularios. La implementación planificada de una estructura de formulario define la secuencia de pasos de este. ![Ejemplo de secuencia de formulario de varios pasos](assets/formpipeline.png)

Ejemplo de secuencia de formulario de varios pasos

Veamos un caso de uso en el que debe crear una secuencia para los pasos de rellenado, verificación, firma y confirmación de un formulario. Para crear dicha secuencia, los pasos son los siguientes:

1. Defina una plantilla de formulario y añádale el panel requerido. Debe haber un panel para cada uno de los pasos de la secuencia. No obstante, puede incluir subpaneles dentro de un mismo panel.

   En este ejemplo, se pueden añadir los siguientes paneles:

   * **Rellenado**: contiene campos de formulario para capturar datos. Aquí puede incluir subpaneles anidados para crear secciones para distintos tipos de información, como personal, familiar y financiera.

   * **Verificar**: contiene el componente **Verificar**, que se puede utilizar en un formulario adaptable basado en XFA. Muestra la información capturada en el panel Relleno en el modo de solo lectura para la verificación.

   * **Firma electrónica**: contiene el componente **Firma**, que se puede utilizar en un formulario adaptable basado en XFA. Proporciona los siguientes servicios de firma:

      * Servicios de firma electrónica de Adobe Document Cloud
      * Firma manuscrita

   * **Confirmación**: contiene el componente **Resumen** que muestra un mensaje que confirma el envío del formulario una vez que el usuario lo ha firmado y llega al paso Confirmación (Resumen) de la secuencia. Los autores pueden configurar el texto del componente Resumen, mostrar un mensaje de agradecimiento, mostrar un vínculo al PDF generado, etc.

1. Establezca el diseño del panel raíz como **[!UICONTROL Asistente]**.
1. Complete los pasos restantes para poder crear la plantilla de formulario. Ver [Crear una plantilla de formulario adaptable personalizada](../../forms/using/custom-adaptive-forms-templates.md).

Una vez definida la secuencia del formulario en la plantilla de formulario, puede utilizarla para crear formularios que tengan la estructura básica definida como la secuencia en contexto. Siempre puede personalizar el formulario para adaptarlo a sus necesidades.
