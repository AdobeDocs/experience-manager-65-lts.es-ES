---
title: 'Tutorial: Crear fragmentos de documento'
description: Crear fragmentos de documento para la comunicación interactiva
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 73%

---

# Tutorial: Crear fragmentos de documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Este tutorial es un paso en la serie [Crear su primera comunicación interactiva](/help/forms/using/create-your-first-interactive-communication.md). Adobe recomienda seguir la serie en secuencia cronológica para comprender, realizar y mostrar el caso de uso completo del tutorial.

Los fragmentos de documento son componentes reutilizables de una correspondencia que se utilizan para componer una comunicación interactiva. Los fragmentos del documento son de los siguientes tipos:

* Texto: un recurso de texto es un fragmento de contenido que consta de uno o más párrafos de texto. Un párrafo puede ser estático o dinámico.
* Lista: es un grupo de fragmentos de documento, que incluyen texto, listas, condiciones e imágenes.
* Condición: las condiciones permiten definir qué contenido se incluye en la comunicación interactiva en función de los datos recibidos del modelo de datos de formulario.

Este tutorial le guiará por los pasos para crear varios fragmentos de documento de texto basados en la anatomía proporcionada en la sección [Planificar la comunicación interactiva](/help/forms/using/planning-interactive-communications.md). Al final de este tutorial, debería poder hacer lo siguiente:

* Crear fragmentos de documento
* Crear variables
* Crear y aplicar reglas

![text_document_fragments](assets/text_document_fragments.gif)

A continuación se muestra la lista de fragmentos de documento creados en este tutorial:

* [Detalles de la factura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Detalles del cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Resumen de la factura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Resumen de cargos](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Cada fragmento de documento incluye campos con texto estático, datos recibidos del modelo de datos de formulario y datos introducidos mediante la interfaz de usuario del agente. Todos estos campos se han representado en la sección [Planificar la comunicación interactiva](/help/forms/using/planning-interactive-communications.md).

Al crear fragmentos de documento en este tutorial, las variables se crean para campos que reciben datos mediante la interfaz de usuario del agente.

Use **FDM_Create_First_IC**, tal como se describe en la sección [Crear un modelo de datos de formulario](../../forms/using/create-form-data-model0.md), como modelo de datos de formulario para crear fragmentos de documento en este tutorial.

## Paso 1: Crear fragmento de documento Detalles de la factura {#step-create-bill-details-text-document-fragment}

El fragmento de documento Detalles de la factura incluye los siguientes campos:

| Campo | Fuente de datos |
|---|---|
| N.º de factura | IU del Agente |
| Período de facturación | IU del Agente |
| Fecha de la factura | IU del Agente |
| Su plan | Modelo de datos de formulario |

Para crear variables para campos con la interfaz de usuario del agente como fuente de datos, crear texto estático y utilizar elementos del modelo de datos de formulario en el fragmento de documento, haga lo siguiente:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.

1. Seleccione **Crear** > **Texto**.
1. Especifique la siguiente información:

   1. Escriba **bill_details_first_ic** como el nombre en el campo **Título**. El título se rellena automáticamente en el campo **Nombre**.

   1. Seleccione **Modelo de datos de formulario** de la sección **Modelo de datos**.

   1. Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y seleccione **Seleccionar**.

   1. Seleccione **Siguiente**.

1. Seleccione la ficha **Variables** en el panel izquierdo y seleccione **Crear**.
1. En la sección **Crear variable**:

   1. Escriba **Invoicenumber** como nombre de la variable.
   1. Seleccione **Cadena** como tipo.
   1. Seleccione **Crear**.

   ![Crear variable de tipo Cadena](assets/variable_create_string_new.png)

   Repita los pasos 4 y 5 para crear las siguientes variables:

   * Billperiod: Tipo Cadena
   * BillDate: Tipo Fecha

   ![Detalles de la factura](assets/variable_bill_details_new.png)

1. Cree texto estático para los siguientes campos mediante el panel derecho:

   * N.º de factura
   * Período de facturación
   * Fecha de la factura
   * Su plan

   ![Texto estático](assets/variable_bill_details_static_text_new.png)

1. Coloque el cursor junto al campo **Número de factura** y haga doble clic en la variable **InvoiceNumber** desde la pestaña **Variables** en el panel izquierdo.
1. Coloque el cursor junto al campo **Período de facturación** y haga doble clic en la variable **Billperiod**.
1. Coloque el cursor junto al campo **Fecha de factura** y haga doble clic en la variable **Fecha de factura**.
1. Seleccione la pestaña **Objetos del modelo de datos** en el panel izquierdo.
1. Coloque el cursor junto al campo **Su plan** y haga doble clic en la propiedad **cliente** > **customerplan**.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Haga clic en **Guardar** para crear el fragmento de documento Detalles de la factura.

## Paso 2: Crear fragmento de documento Detalles del cliente {#step-create-customer-details-text-document-fragment}

El fragmento de documento Detalles del cliente incluye los siguientes campos:

| Campo | Fuente de datos |
|---|---|
| Nombre del cliente | Modelo de datos de formulario |
| Dirección | Modelo de datos de formulario |
| Lugar de suministro | IU del Agente |
| Código de estado | IU del Agente |
| Número de móvil | Modelo de datos de formulario |
| Número de contacto alternativo | Modelo de datos de formulario |
| Número de relación | Modelo de datos de formulario |
| Número de conexiones | IU del Agente |

Para crear variables para campos con la interfaz de usuario del agente como fuente de datos, crear texto estático y utilizar elementos del modelo de datos de formulario en el fragmento de documento, haga lo siguiente:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Seleccione **Crear** > **Texto**.
1. Especifique la siguiente información:

   1. Escriba **customer_details_first_ic** como el nombre en el campo **Título**. El título se rellena automáticamente en el campo **Nombre**.

   1. Seleccione **Modelo de datos de formulario** de la sección **Modelo de datos**.

   1. Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y seleccione **Seleccionar**.

   1. Seleccione **Siguiente**.

1. Seleccione la ficha **Variables** en el panel izquierdo y seleccione **Crear**.
1. En la sección **Crear variable**:

   1. Escriba **Placesupply** como nombre de la variable.
   1. Seleccione **Cadena** como tipo.
   1. Seleccione **Crear**.

   Repita los pasos 4 y 5 para crear las siguientes variables:

   * Código de estado: Tipo Número
   * Numberconnections: Tipo Número

1. Seleccione la pestaña **Objetos del modelo de datos**, coloque el cursor en el panel derecho y haga doble clic en la propiedad **cliente** > **nombre**.
1. Pulse Entrar para mover el cursor a la línea siguiente y haga doble clic en la propiedad **cliente** > **dirección**.
1. Cree texto estático para los siguientes campos mediante el panel derecho:

   * Número de móvil
   * Número de contacto alternativo
   * Lugar de suministro
   * Número de relación
   * Código de estado
   * Número de conexiones

   ![El cliente detalla el texto estático](assets/customer_details_static_text_new.png)

1. Coloque el cursor junto al campo **Número de móvil** y haga doble clic en la propiedad **cliente** > **mobilenum**.
1. Coloque el cursor junto al **Número de contacto alternativo** y haga doble clic en la propiedad **&#x200B; cliente** > **alternatemobilenumber**.
1. Coloque el cursor junto al campo **Número de relación** y haga doble clic en la propiedad **cliente** > **relationshipnumber**.
1. Seleccione la pestaña **Variables**, coloque el cursor junto al campo **Lugar de suministro** y haga doble clic en la variable **Placesupply**.
1. Coloque el cursor junto al campo **Código de estado** y haga doble clic en la variable **Statecode**.
1. Coloque el cursor junto al campo **Número de conexiones** y haga doble clic en la variable **Numberconnections**.

   ![Detalles del cliente](assets/customer_details_df2_new.png)

1. Haga clic en **Guardar** para crear el fragmento de documento de texto Detalles del cliente.

## Paso 3: Crear fragmento de documento Resumen de la factura {#step-create-bill-summary-text-document-fragment}

El fragmento de documento Resumen de la factura incluye los siguientes campos:

| Campo | Fuente de datos |
|---|---|
| Saldo anterior | IU del Agente |
| Pagos | IU del Agente |
| Ajustes | IU del Agente |
| Cargos del período de facturación actual | Modelo de datos de formulario |
| Importe vencido | IU del Agente |
| Fecha de vencimiento | IU del Agente |

Para crear variables para campos con la interfaz de usuario del agente como fuente de datos, crear texto estático y utilizar elementos del modelo de datos de formulario en el fragmento de documento, haga lo siguiente:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Seleccione **Crear** > **Texto**.
1. Especifique la siguiente información:

   1. Escriba **bill_summary_first_ic** como nombre en el campo **Título**. El título se rellena automáticamente en el campo **Nombre**.

   1. Seleccione **Modelo de datos de formulario** de la sección **Modelo de datos**.

   1. Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y seleccione **Seleccionar**.

   1. Seleccione **Siguiente**.

1. Seleccione la ficha **Variables** en el panel izquierdo y seleccione **Crear**.
1. En la sección **Crear variable**:

   1. Escriba **Saldo anterior** como nombre de la variable.
   1. Seleccione **Número** como tipo.
   1. Seleccione **Crear**.

   Repita los pasos 4 y 5 para crear las siguientes variables:

   * Pagos: Tipo Número
   * Ajustes: Tipo Número
   * Amountdue: Tipo Número
   * Duedate: Tipo Fecha

1. Cree texto estático para los siguientes campos mediante el panel derecho:

   * Saldo anterior
   * Pagos
   * Ajustes
   * Cargos del período de facturación actual
   * Importe vencido
   * Fecha de vencimiento
   * Cargos por pago atrasado después de la fecha de vencimiento es de $ 20

   ![Texto estático de Resumen de la factura](assets/bill_summary_static_new.png)

1. Coloque el cursor junto al campo **Saldo anterior** y haga doble clic en la variable **Previousbalance**.
1. Coloque el cursor junto al campo **Pagos** y haga doble clic en la variable **Pagos**.
1. Coloque el cursor junto al campo **Ajustes** y haga doble clic en la variable **Ajustes**.
1. Coloque el cursor junto al campo **Importe adeudado** y haga doble clic en la variable **Amountdue**.
1. Coloque el cursor junto al campo **Fecha de vencimiento** y haga doble clic en la variable **Duedate**.
1. Seleccione la pestaña **Objetos del modelo de datos**, coloque el cursor junto al campo **Gastos del período de la factura actual** en el panel derecho y haga doble clic en la propiedad **facturas** > **usagecharges**.

   ![Resumen de la factura](assets/bill_summary_static_variables_new.png)

1. Haga clic en **Guardar** para crear el fragmento de documento de texto Detalles del cliente.

## Paso 4: Crear fragmento de documento Resumen de gastos {#step-create-summary-of-charges-text-document-fragment}

El fragmento de documento Resumen de gastos incluye los siguientes campos:

| Campo | Fuente de datos |
|---|---|
| Cargos por llamadas | Modelo de datos de formulario |
| Cargos por llamadas de conferencia | Modelo de datos de formulario |
| Cargos por SMS | Modelo de datos de formulario |
| Cargos por Internet móvil | Modelo de datos de formulario |
| Cargos de itinerancia nacional | Modelo de datos de formulario |
| Cargos de itinerancia internacional | Modelo de datos de formulario |
| Cargos por servicios de valor añadido | Modelo de datos de formulario |
| Cargos totales | Modelo de datos de formulario |
| TOTAL A PAGAR | Modelo de datos de formulario |

Para crear texto estático y utilizar elementos del modelo de datos de formulario en el fragmento de documento, haga lo siguiente:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Seleccione **Crear** > **Texto**.
1. Especifique la siguiente información:

   1. Escriba **summary_charges_first_ic** como nombre en el campo **Título**. El título se rellena automáticamente en el campo Nombre.

   1. Seleccione **Modelo de datos de formulario** de la sección **Modelo de datos**.

   1. Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y seleccione **Seleccionar**.

   1. Seleccione **Siguiente**.

1. Cree texto estático para los siguientes campos mediante el panel derecho:

   * Cargos por llamadas
   * Cargos por llamadas de conferencia
   * Cargos por SMS
   * Cargos por Internet móvil
   * Cargos de itinerancia nacional
   * Cargos de itinerancia internacional
   * Cargos por servicios de valor añadido
   * Cargos totales
   * TOTAL A PAGAR

   ![Resumen de gastos](assets/summary_charges_static_new.png)

1. Seleccione la pestaña **Objetos del modelo de datos**.
1. Coloque el cursor junto al campo **Gastos de llamada** y haga doble clic en la propiedad **facturas** > **callcharges**.
1. Coloque el cursor junto al campo **Gastos por llamadas de conferencia** y haga doble clic en la propiedad **facturas** > **confcallcharges**.
1. Coloque el cursor junto al campo **Gastos por SMS** y haga doble clic en la propiedad **facturas** > **smscharge**.
1. Coloque el cursor junto al campo **Gastos por Internet móvil** y haga doble clic en la propiedad **facturas** > **internetcharges**.
1. Coloque el cursor junto al campo **Gastos de itinerancia nacional** y haga doble clic en la propiedad **facturas** > **roamingnational**.
1. Coloque el cursor junto al campo **Gastos de itinerancia internacional** y haga doble clic en la propiedad **facturas** > **roamingintnl**.
1. Coloque el cursor junto al campo **Gastos por servicios de valor agregado** y haga doble clic en la propiedad **facturas** > **vas**.
1. Coloque el cursor junto al campo **Gastos totales** y haga doble clic en la propiedad **facturas** > **usagecharges**.
1. Coloque el cursor junto al campo **TOTAL A PAGAR** y haga doble clic en la propiedad **facturas** > **usagecharges**.

   ![Resumen de gastos](assets/summary_charges_static_fdm_new.png)

1. Seleccione el texto de la fila **Gastos por servicios de valor agregado** y seleccione **Crear regla** para crear una condición basada en la cual se muestre la fila en la comunicación interactiva:
1. En la ventana emergente **Crear regla**:

   1. Seleccione **Modelos y variables de datos** y luego **facturas** > **callcharges**.

   1. Seleccione **es menor que** como operador.
   1. Seleccione **Número** y escriba el valor como **60**.

   En función de esta condición, la fila Gastos de servicios de valor agregado solo se muestra si el valor del campo Gastos de llamadas es inferior a 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Haga clic en **Guardar** para crear el fragmento de documento Resumen de gastos.
