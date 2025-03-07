---
title: Registre una transacción para la API de componente personalizada para AEM Forms en JEE.
description: Obtenga información acerca del uso de la API TransactionRecorder para registrar transacciones de componentes personalizados.
feature: Transaction Reports
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: e2d1b548-ce30-471b-b01c-ce37b737aeb5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Registre una transacción para las API de componentes personalizadas para AEM Forms en JEE {#record-a-transaction-for-custom-components}

Al utilizar API facturables en el componente personalizado, puede habilitar la creación de informes de transacciones para el componente. Para habilitar los informes de transacciones, modifique el archivo `component.xml` del componente y agregue la etiqueta que se indica a continuación en la operación para la cual se deben habilitar los informes de transacciones.

**Etiqueta**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Etiqueta de operación antigua | Nueva etiqueta de operación |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Si debe capturar más de una transacción para una API, como una API por lotes en la que el recuento de transacciones varía según el número de recuentos de entrada, administre el recuento de transacciones en el nivel de API.

**Para registrar el recuento de transacciones variadas:**

1. Importe la clase `"com.adobe.idp.dsc.InvocationContextStack"` en el código. La clase forma parte del archivo del SDK `adobe-livecycle-client.jar`. El archivo del SDK está disponible en `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Actualice el archivo de cliente compartido anteriormente en el proyecto de cliente con el nuevo archivo en caso de que ya esté empaquetado.

1. En la API para la cual se deben registrar varias transacciones:
   1. Agregue lógica para poder almacenar el recuento de transacciones en alguna variable entera, como `transaction_count`.
   1. Cuando la operación se realice correctamente, agregue `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Artículos relacionados

* [Activación y visualización de informes de transacciones para AEM Forms en JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista de API facturables para AEM Forms en JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
