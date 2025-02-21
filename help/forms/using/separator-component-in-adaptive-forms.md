---
title: Componente Separador en formularios adaptables
description: Puede utilizar el componente Separador para separar visualmente las secciones de un formulario.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 86%

---

# Componente Separador en formularios adaptables{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. En este artículo se describe un método antiguo para crear Forms adaptable mediante componentes de base. </span>

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto general y el estilo de un componente separador especificando las siguientes propiedades del componente separador:

* **Nombre del elemento:** especifica el nombre del componente. Las expresiones SOM se dirigen al componente con el valor especificado en el campo Nombre del elemento.
* **Grosor:** especifica el grosor del componente Separador en píxeles.

* **Clase CSS:** especifica la clase CSS personalizada para el componente Separador.

* **Estilos en línea:** con AEM Forms, ahora puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente Separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar las propiedades de un componente separador:

1. Seleccione un componente separador y seleccione ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una pestaña de la sección Propiedades CSS en línea para especificar las propiedades CSS. Por ejemplo: a. En la pestaña Campo, haga clic en **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **border**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **negro sólido de 3 píxeles**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Haga clic en **Vista previa** para obtener una vista previa de los cambios en el formulario.
1. Haga clic en **Aceptar** si desea confirmar los cambios o en **Cancelar** para salir del cuadro de diálogo sin ningún cambio.
