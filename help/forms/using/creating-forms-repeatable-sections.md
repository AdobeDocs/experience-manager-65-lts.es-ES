---
title: Crear formularios con secciones repetibles
description: Las secciones repetibles son paneles que se pueden añadir o quitar dinámicamente a un formulario.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 100%

---

# Crear formularios con secciones repetibles {#creating-forms-with-repeatable-sections}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

Las secciones repetibles son paneles que se pueden añadir o quitar dinámicamente a un formulario.

Por ejemplo, mientras se postula para un trabajo, el buscador de empleo aporta detalles de empleo previos, como el nombre de la empresa, la función, el proyecto y otra información. La información de todos los empleadores requiere secciones diferentes pero parecidas. En ese escenario, el formulario de empleo incluye una sección de empleadores y también ofrece la opción de añadir dinámicamente más secciones de ese tipo. Estas secciones, que se añaden dinámicamente, se conocen como secciones repetibles.

Puede utilizar uno de los siguientes métodos para crear paneles repetibles:

## Utilizar Instance Manager mediante scripts  {#using-instance-manager-via-scripts-nbsp}

1. En el modo de edición, seleccione un panel y seleccione ![cmppr](assets/cmppr.png). En la barra lateral, en Propiedades, habilite **Hacer que el panel sea repetible**. Especifique los valores para los campos **[!UICONTROL Máximo]** y **[!UICONTROL Mínimo]**.

   El campo Máximo especifica el número máximo de veces que puede aparecer un panel en la página. Puede especificar -1 en el campo Máximo para permitir que el panel aparezca durante un número infinito de veces.

   El campo Mínimo especifica el número mínimo de veces que aparece un panel en el formulario. Si establece el campo Mínimo en cero, más adelante, puede quitar todas las instancias mediante scripts una vez completada la representación.

   >[!NOTE]
   >
   >Para crear un panel no repetible, establezca el valor del campo Máximo y Mínimo en uno. El diseño del acordeón no es compatible con -1 en el campo Máximo. Puede especificar un número elevado para dar la noción de valor infinito.

1. El elemento principal del panel, que se va a repetir, debe contener botones de añadir y eliminar para administrar las instancias de los paneles repetibles. Realice los siguientes pasos para insertar botones en el elemento principal y habilitar scripts en los botones:

   1. Desde la barra lateral, arrastre y suelte un componente de botón en el elemento principal del panel. Seleccione el componente y seleccione ![edit-rules](assets/edit-rules.png). Las reglas del botón se abren en el editor de reglas.
   1. En la ventana Editor de reglas, haga clic en **Crear**.

      Seleccione **Editor visual** en la fila Objetos y funciones de formularios.

      1. En el área de regla, en CUANDO, **se hace clic** en seleccionar estado.
      1. En ENTONCES:

         * Para crear un botón de añadir panel, seleccione **Añadir instancia** y arrastre el panel utilizando el ![panel lateral de alternancia](assets/toggle-side-panel.png) o selecciónelo utilizando **Colocar objeto o seleccionar aquí.**
         * Para crear un botón de eliminar panel, seleccione **Quitar instancia** y arrastre el panel utilizando el ![panel lateral de alternancia](assets/toggle-side-panel.png) o selecciónelo utilizando **Colocar objeto o seleccionar aquí.**

      Seleccione **Editor de código** en la fila Objetos y funciones de formularios. Haga clic en **Editar reglas** y en el área de código:

      * Para crear un botón de añadir panel, especifique `this.panel.instanceManager.addInstance()`
      * Para crear un botón de eliminar panel, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Haga clic en **Listo**.

      >[!NOTE]
      >
      >Si un campo pertenece a un panel repetible, no puede acceder a él directamente utilizando su nombre en los scripts. Para acceder al campo, especifique la instancia repetible a la que pertenece el campo utilizando la API de `instances` en `InstanceManager`. La sintaxis para usar la API de `instances` en `InstanceManager` es la siguiente:
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Por ejemplo, crea un formulario adaptable con un panel repetible que tiene un cuadro de texto. Cuando rellene automáticamente el formulario con tres cuadros de texto repetibles, necesitará el siguiente xml:
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >Para leer datos de AA1, especifique:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Para leer datos de AA2, especifique:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Para obtener más información, consulte: Clase: InstanceManager#instances en [Referencia de la API de Java de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).

      >[!NOTE]
      >
      >Cuando todas las instancias de un panel se quiten de un formulario adaptable, para agregar una instancia del panel quitado, utilice la sintaxis _panelName para capturar el Instance Manager del panel y use la API addInstance de Instance Manager para agregar la instancia eliminada. Por ejemplo, _panelName.addInstance(). Añade una instancia del panel eliminado.

## Usar el diseño de acordeón para el panel principal   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Un panel tiene varias opciones de diseño. La opción Diseño para el diseño de acordeón es compatible de forma predeterminada con los paneles repetibles. Realice los siguientes pasos en el panel repetible con la opción Diseño para el diseño de acordeón:

1. En el panel principal que se va a repetir, seleccione ![cmppr](assets/cmppr.png). Puede ver las propiedades en la barra lateral. En la lista desplegable **Diseño**, seleccione **Acordeón**.
1. En un panel que se va a repetir, seleccione ![cmppr](assets/cmppr.png). Puede ver las propiedades del panel en la barra lateral. Habilite la pestaña **Hacer que el panel sea repetible** y especifique los valores para los campos **Máximo** y **Mínimo**.

   Ahora puede utilizar los botones más (+) y eliminar (![eliminar panel](assets/delete-panel.png)) para añadir y quitar los paneles.

## Usar subformularios repetibles de la plantilla de formulario (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

El subformulario repetible es similar a los paneles repetibles de los formularios adaptables. En AEM Forms Designer, realice los siguientes pasos para crear un subformulario repetible:

1. En la paleta Jerarquía, seleccione el subformulario principal del subformulario que desea que se repita.
1. En la paleta Objeto, haga clic en la pestaña Subformulario y seleccione De posición variable en la lista Contenido.
1. Seleccione el subformulario que desea repetir.
1. En la paleta Objeto, haga clic en la pestaña Subformulario y seleccione De posición variable o De posición fija en la lista Contenido.
1. Haga clic en la pestaña Enlace y seleccione Repetir subformulario para cada elemento de datos.
1. Para especificar el número mínimo de repeticiones, seleccione Mínimo y escriba un número en el cuadro correspondiente. Si la opción se ajusta a 0 y no se suministran datos para los objetos del subformulario en el momento de la combinación de datos, el subformulario no se coloca al procesar el formulario.
1. Para especificar el número máximo de repeticiones de subformulario, seleccione Máx. y escriba un número en el cuadro correspondiente. Si no se especifica un valor en el cuadro Máx., el número de repeticiones de subformulario es ilimitado.
1. Para especificar un número definido de repeticiones de subformulario, independientemente de la cantidad de datos, seleccione la opción Recuento inicial y escriba un número en el cuadro correspondiente. Si se selecciona esta opción y no hay ningún dato disponible o existen menos entradas de datos que el valor especificado en Recuento inicial, las instancias vacías del subformulario todavía se colocan en el formulario.
1. Agregue dos botones en el subformulario principal: uno para añadir instancias y otro para eliminar instancias de subformularios repetibles. Para ver los pasos detallados, consulte [Generar una acción](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Ahora, vincule la plantilla del formulario al formulario adaptable. Para ver los pasos detallados, consulte [Crear un formulario adaptable basado en una plantilla](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Utilice los botones creados en el paso 9 para añadir y quitar subformularios.

El archivo .zip adjunto contiene un subformulario repetible de ejemplo.

[Obtener archivo](assets/samplerepeatablesubform.zip)

## Utilizar la configuración repetida de un esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Puede crear paneles repetibles a partir de un esquema XML y de la propiedad minOccours y maxOccurs de cualquier elemento de tipo complejo. Para obtener información detallada sobre el esquema XML, consulte [Crear formularios adaptables mediante el esquema XML como modelo de formulario](/help/forms/using/adaptive-form-xml-schema-form-model.md).

En el siguiente código, el panel `SampleType` utiliza la propiedad minOccours y maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Para los diseños que no son de acordeón, utilice los componentes de botón del formulario adaptable para agregar y quitar instancias.
