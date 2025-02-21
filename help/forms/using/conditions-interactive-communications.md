---
title: Condiciones de las comunicaciones interactivas
description: 'Crear y editar fragmentos de condición para utilizarlos en comunicaciones interactivas: la condición es uno de los cuatro tipos de fragmentos de documento utilizados para crear comunicaciones interactivas. Los otros tres son textos, listas y fragmentos de diseño.'
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 77%

---

# Condiciones de las comunicaciones interactivas{#conditions-in-interactive-communications}

Crear y editar fragmentos de condición para utilizarlos en comunicaciones interactivas: la condición es uno de los cuatro tipos de fragmentos de documento utilizados para crear comunicaciones interactivas. Los otros tres son textos, listas y fragmentos de diseño.

## Información general {#overview}

La condición es un fragmento de documento que puede incluir en una comunicación interactiva. Los demás fragmentos de documento son [texto](../../forms/using/texts-interactive-communications.md), lista y fragmento de diseño. Las condiciones permiten definir uno o varios recursos contextuales que se incluyen en una comunicación interactiva en función de los datos y las reglas suministrados.

Ejemplos:

* En la instrucción de extracto de la tarjeta de crédito, se indicará la cuota anual y la imagen de la tarjeta de crédito en función del tipo de tarjeta del cliente.
* En un recordatorio del seguro, se muestran cálculos de impuestos basados en el estado de los impuestos del cliente.

Los recursos en las condiciones que se procesan en función de las reglas aplicadas y los valores aprobados para la regla. Las reglas de las condiciones pueden comprobar los valores en los siguientes tipos de datos:

* Propiedad del modelo de datos de formulario asociado
* Todas las variables que cree en la condición
* Cadenas
* Números
* Expresiones matemáticas
* Fechas

## Crear condición {#createcondition}

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Condición]**.
1. Especifique la siguiente información:

   * **[!UICONTROL Título]**: (Opcional) Escriba el título de la condición. Los títulos no tienen por qué ser únicos, y pueden contener caracteres especiales y caracteres que no sean de inglés. Las condiciones son referidas mediante sus títulos (cuando están disponibles), como en miniaturas y propiedades.
   * **[!UICONTROL Nombre]**: nombre exclusivo de la condición, dentro de una carpeta. No pueden existir dos fragmentos de documento (texto, condición o lista) con el mismo nombre dentro de una carpeta. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título. Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en Nombre, puede editarlo.

   * **[!UICONTROL Descripción]**: escriba una descripción del fragmento del documento.
   * **[!UICONTROL Modelo de datos de formulario]**: de forma opcional, seleccione el botón Modelo de datos de formulario para crear la condición basada en un modelo de datos de formulario. Al seleccionar el botón Modelo de datos de formulario, aparecerá el campo **[!UICONTROL Modelo de datos de formulario]**. Busque y seleccione un modelo de datos de formulario. Al crear una condición para una comunicación interactiva, asegúrese de utilizar el mismo modelo de datos que desea utilizar en la comunicación interactiva. Para obtener información sobre el modelo de datos de formulario, consulte [Integración de datos](../../forms/using/data-integration.md).

   * **[!UICONTROL Etiquetas]**: de forma opcional, para crear una etiqueta personalizada, escriba un valor en el campo de texto y seleccione Entrar. Al guardar esta condición, se crean las etiquetas recién agregadas.

1. Seleccione **[!UICONTROL Siguiente]**.

   Aparecerá la página Crear condición.

   ![createcondition](assets/createcondition.png)

1. Seleccione **[!UICONTROL Agregar Assets]**.

   Aparecerá la página Seleccionar recursos y mostrará los textos, las listas, las condiciones y las imágenes disponibles para agregar en la condición.

   >[!NOTE]
   >
   >En la página Seleccionar Assets solo aparecen los recursos basados en ninguno, los recién creados y los basados en FDM (creados con el mismo FDM que la condición que crea).

1. Seleccione los recursos adecuados para seleccionarlos e incluirlos en la condición y, a continuación, seleccione **[!UICONTROL Listo]**.

   Aparecerá la página Crear condición y se enumerarán los recursos agregados.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Puede utilizar las siguientes opciones para administrar recursos en una condición:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] Rechazar cambio.** Seleccione este icono para rechazar los cambios que puede haber realizado en el recurso y en la regla de la condición.
   **[B] Aceptar cambio.** Seleccione este icono para aceptar los cambios realizados en el recurso y en la regla de la condición.
   **[C] Duplicar recurso.** Seleccione este icono para crear una copia del recurso junto con la regla aplicada, si la hay, en la condición. A continuación, puede editar la regla y el recurso para los recursos duplicados. Duplicar un recurso resulta útil para crear reglas similares que muestren recursos alternativos basados en un contexto en particular.
   **[D] Mostrar vista previa.** Seleccione este icono para mostrar una vista previa del recurso en la página Crear/Editar condición.
   **Reordenar “servidor”.**: seleccione y mantenga presionado este icono para arrastrar y soltar recursos para reordenarlos dentro de una condición.

   Puede seleccionar las siguientes opciones para especificar el comportamiento de la condición durante la ejecución:

   * **Evaluación de varios resultados deshabilitada\Evaluación de varios resultados habilitada**: cuando esta opción esté habilitada (aparece como “Evaluación de varios resultados habilitada”), todas las reglas se evaluarán y el resultado será la suma de todas las reglas que se encuentren como true. Si esta opción está deshabilitada (aparece como “Evaluación de varios resultados deshabilitada”), solo se evaluará la primera regla que se encuentre como true y se convertirá en el resultado de la condición.

   * **Salto de página**: seleccione esta opción ( ![break](assets/break.png)) para agregar un salto de página entre los recursos de las condiciones. Cuando esta opción no esté seleccionada ( ![nobreak](assets/nobreak.png)), si una condición se pasa a la siguiente página de la salida de impresión, toda la condición se pasará a la siguiente página en lugar de romperse en la página entre los recursos de la condición.

1. Seleccione **[!UICONTROL Crear regla]** para agregar reglas para mostrar u ocultar los recursos, según sea necesario. Para utilizar variables en las reglas, consulte [Crear variables](#variables). Para obtener más información, consulte [Agregar reglas a una condición](#ruleeditor).

   Las reglas creadas aparecen en la columna REGLA de la pantalla Crear condición.

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Puede insertar recursos en la condición que ya tengan reglas o que se repitan.

1. Seleccione **[!UICONTROL Guardar]**.

   Se creará la condición. Ahora puede usar la condición como un bloque de creación al crear una comunicación interactiva.

   >[!NOTE]
   >
   >Para guardar una condición nueva o editada, debe tener al menos una regla para cada uno de los recursos agregados en la condición.

## Editar una condición {#edit-a-condition}

Puede editar una condición si sigue los siguientes pasos. También puede editar una condición desde una comunicación interactiva si selecciona Editar fragmento en el menú emergente.

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Navegue hasta la condición y selecciónela.
1. Seleccione **[!UICONTROL Editar]**.
1. Realice los cambios necesarios en la condición. Para obtener más información sobre la información que puede cambiar en una condición, consulte [Crear condición](#createcondition).
1. Seleccione **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Cerrar]**.

## Crear reglas en condición {#ruleeditor}

Con el editor de reglas en una condición, puede crear reglas para mostrar u ocultar recursos en función de **condiciones preestablecidas**. Estas condiciones se pueden construir en función de lo siguiente:

* Cadenas
* Números
* Expresiones matemáticas
* Fechas
* Propiedades del modelo de datos de formulario asociado
* Cualquier [variable](#variables) que puede haber creado

### Crear regla en condición {#create-rule-in-condition}

1. Al crear o editar una condición, seleccione el icono ![ruleeditoricon](assets/ruleeditoricon.png) (Editor de reglas) para el recurso correspondiente.

   Aparecerá el cuadro de diálogo Crear regla. Además de Cadena, Número, Expresión matemática y Fecha, también están disponibles las siguientes reglas en el editor de reglas para crear instrucciones:

   * Propiedades del modelo de datos de formulario asociado
   * Cualquier [variable](#variables) que puede haber creado.

   ![createruledialog](assets/createruledialog.png)

   Seleccione la opción adecuada que desea evaluar.

   >[!NOTE]
   >
   >La propiedad Colección no es compatible con la creación de reglas para mostrar recursos.

1. Seleccione el operador apropiado para evaluar la regla, como Es igual a, Contiene y Comienza con.
1. Inserte la expresión, cadena, propiedad, variable o fecha del modelo de datos de evaluación.

   ![Regla para mostrar un recurso cuando el tipo de directiva es estándar](assets/ruleincondition.png)

   Regla para mostrar un recurso cuando el tipo de directiva es estándar

   * Al crear o editar una regla, también puede seleccionar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla/Editar regla. El cuadro de diálogo expandido a ventana completa le permite crear [variables](#variables) para construir reglas. Vuelva a seleccionar Cambiar tamaño para volver al cuadro de diálogo normal Crear regla.

   * También puede crear varias condiciones en una regla.

1. Seleccione **[!UICONTROL Listo]**.

   La regla se aplicará al recurso.

## Crear y usar variables en una condición {#variables}

Al crear o editar una regla en una condición, puede seleccionar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla\Editar regla. El cuadro de diálogo expandido a ventana completa le permite:

* Crear y usar variables en la regla
* Arrastrar y soltar las propiedades y variables del modelo de datos de formulario en la regla

Vuelva a seleccionar Cambiar tamaño para volver al cuadro de diálogo Crear regla\Editar regla.

### Crear variables {#create-variables}

1. Al crear o editar una regla en una condición, puede seleccionar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla\Editar regla.

   Aparecerá el cuadro de diálogo expandido y a ventana completa.

   ![expandededitruledialog](assets/expandededitruledialog.png)

1. En el panel izquierdo, seleccione **[!UICONTROL Variables]**.

   Aparecerá el panel Variables.

   ![expandededitrulevariables](assets/expandededitrulevariables.png)

1. Seleccione **[!UICONTROL Crear]**.

   Aparecerá el panel Crear variables.

1. Escriba la siguiente información y seleccione **[!UICONTROL Crear]**:

   * **[!UICONTROL Nombre]**: nombre de la variable.
   * **[!UICONTROL Descripción]**: opcionalmente, introduzca una descripción sobre la variable.
   * **[!UICONTROL Tipo]**: seleccione un tipo de variable: cadena, número, booleano o fecha.
   * **[!UICONTROL Permitir solo valores específicos]**: para las variables cadena y número, puede asegurarse de que el agente elija entre un conjunto específico de valores para un marcador de posición en la interfaz de usuario de Agente. Para especificar el conjunto de valores, seleccione esta opción y, a continuación, especifique los valores separados por coma que están permitidos en el campo **[!UICONTROL Valores]**.

1. Seleccione **[!UICONTROL Crear]**.

   La variable se crea y se enumera en el panel Variables.

1. Para insertar una variable en la regla, arrastre y suelte la variable en un marcador de posición para una opción de la regla.
1. Después de crear una regla válida, seleccione **[!UICONTROL Listo]**.

   Realice más cambios, si es necesario, en la condición y guárdela.
