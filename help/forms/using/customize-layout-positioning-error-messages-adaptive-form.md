---
title: Personalizar la presentación y la colocación de los mensajes de error de un formulario adaptable
description: Puede personalizar el diseño y la posición de los mensajes de error de un formulario adaptable.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 56%

---

# Personalizar la presentación y la colocación de los mensajes de error de un formulario adaptable{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

Puede personalizar la presentación y la posición de los mensajes de error de un formulario adaptable. Puede realizar las siguientes personalizaciones:

* Personalizar la ubicación y el diseño del pie de ilustración de un campo sin cambiar las propiedades CSS correspondientes
* Personalizar la posición de los mensajes de error en línea
* Personalizar el contenido del indicador de ayuda dinámica
* Personalice la posición de los componentes de campo (título, widget, descripción breve, descripción larga y componentes de indicador de ayuda) sin cambiar las propiedades CSS correspondientes

## Personalizar el diseño de los campos {#customize-layout-of-fields}

Puede personalizar el diseño de un solo campo o de todos los campos para cambiar la posición del rótulo y los mensajes de error.

Para aplicar un diseño personalizado a un campo, haga lo siguiente:

### Personalizar el diseño de un solo campo {#customize-layout-of-a-single-field}

1. Abra el formulario en el modo **Estilo**. Para abrir el formulario en modo Estilo, en la barra de herramientas de la página, seleccione ![lista desplegable de lienzo](assets/canvas-drop-down.png) > **Estilo**.
1. En la barra lateral, en **Objetos de formulario**, seleccione el campo y el botón de edición ![edit-button](assets/edit-button.png).
1. Seleccione el estado del campo que desea personalizar y especifique el estilo para ese estado.

   ![Especificar el estilo en línea de un campo](assets/edit-error-state.png)

### Personalizar la presentación de todos los campos de un formulario {#customize-layout-of-all-the-fields-of-a-form}

Con AEM Forms, ahora puede crear una temática y aplicarla al formulario. El editor de temáticas permite especificar el estilo de los componentes del formulario en un lugar. Al crear una temática, se especificará el estilo en un nivel de componente. Para obtener más información sobre las temáticas, consulte [Temáticas en AEM Forms](../../forms/using/themes.md).

Cree una temática con el Editor de temáticas para personalizar la presentación de todos los campos del formulario. Después de crear una temática, realice los siguientes pasos para aplicarla a un formulario:

1. Abra el formulario en modo de edición. 

1. En el modo de edición, seleccione un componente y, a continuación, ![field-level](assets/field-level.png) > **Contenedor de formulario adaptable** y ![cmppr](assets/cmppr.png).
1. En la barra lateral, en Temática de formulario adaptable, seleccione la temática que ha creado con el Editor de temáticas.

## Crear un diseño de campo personalizado {#create-a-custom-field-layout}

1. Abra CRXDE Lite. La dirección URL predeterminada es https://&#39;[server]:[port]&#39;/crx/de.
1. Copie un diseño de campo del nodo /libs/fd/af/layouts/field (por ejemplo, defaultFieldLayout) al nodo /apps (por ejemplo, /apps/af-field-layout).
1. Cambie el nombre del nodo copiado y del archivo defaultFieldLayout.jsp. Por ejemplo, errorOnRight.jsp.

1. Cambie el valor de las propiedades qtip y jcr:description del nodo copiado. Por ejemplo, cambie el valor de las propiedades a Error On Right

1. Para agregar estilos y comportamientos nuevos, cree una biblioteca de cliente en el nodo /etc.

   Por ejemplo, en la ubicación /etc/af-field-layout-clientlib, cree el nodo client-library. Agregue la propiedad categories con el valor af.field.errorOnRight y el archivo style.less con el siguiente código:

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. Para mejorar el aspecto y el comportamiento, incluya la biblioteca de cliente creada en el archivo del diseño (errorOnRight.jsp).
1. Abra el cuadro de diálogo de edición del campo y seleccione la ficha **Estilo**. En el cuadro desplegable **Configuración del diseño del campo**, seleccione el diseño recién creado y haga clic en **Aceptar**.

El paquete ErrorOnRight.zip contiene código para mostrar mensajes de error en el lado derecho de los campos.

[Obtener archivo](assets/erroronright.zip)
