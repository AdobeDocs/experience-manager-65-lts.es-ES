---
title: Información general de informes de transacciones para AEM Forms en JEE
description: Mantenga un recuento de todos los formularios enviados, representados, documentos convertidos en un formato a otro, y más.
feature: Transaction Reports
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Activación y visualización de informes de transacciones para AEM Forms en JEE {#transaction-reports-overview}

<!--Transaction reports in AEM Forms on JEE let you keep a count of all transactions taken place on your AEM Forms deployment. The objective is to provide information about product usage and helps business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of a document
* Rendition of a document
* Conversion of a document from one file format to another 

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis-jee.md). Transaction log helps you to gain information about the number of documents submitted, rendered, and converted.-->

## Habilitar informes de transacciones {#enable-transaction-reporting}

De forma predeterminada, el registro de transacciones está desactivado. Para habilitar los informes de transacciones, realice los siguientes pasos:

1. Vaya a `/adminui` en su AEM Forms en JEE, por ejemplo, `http://10.14.18.10:8080/adminui`.
1. Inicie sesión como **administrador**.
1. Vaya a **Configuración** > **Configuración del sistema principal** > **Configuraciones**.
1. Haga clic en la casilla de verificación para **habilitar los informes de transacciones** y **guardar** la configuración.

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. Reinicie el servidor.
1. Aparte de los cambios en el servidor, en el lado del cliente debe actualizar el archivo `adobe-livecycle-client.jar` en su proyecto, si está utilizando el mismo.

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## Ver informe de transacciones {#view-transaction-report}

Cuando habilita los informes de transacciones, se puede obtener acceso a la información sobre los recuentos de transacciones a través del [informe de transacciones a través del panel](#transaction-report-dashboard) y de un [informe de transacciones detallado a través del archivo de registro](#transaction-report-logfile). Ambos se explican a continuación:

### Informe de transacciones mediante tablero {#transaction-report-dashboard}

El informe de transacciones a través del panel proporciona el número total de transacciones contabilizadas para cada tipo de transacción. Por ejemplo, se obtiene la información sobre el número total de formularios procesados, convertidos y enviados como se muestra en la imagen. Para obtener el informe de transacciones:

1. Vaya a `/adminui` en su AEM Forms en JEE, por ejemplo: `http://10.13.15.08:8080/adminui`.
1. Inicie sesión como **administrador**.
1. Haga clic en Monitor de estado.
1. Vaya a la ficha **Informador de transacciones**, haga clic en **Calcular transacciones totales** y verá que un gráfico circular representa el número de PDF forms enviados, procesados o convertidos.

![sample-transaction-report-jee](assets/transaction-piechart.png)


### Informe de transacciones mediante archivo de registro {#transaction-report-logfile}

El informe de transacciones mediante el archivo de registro proporciona información detallada sobre cada transacción. Para acceder a los registros de transacciones, siga la ruta de contexto relativa al inicio del servidor. De forma predeterminada, las transacciones se capturan en un archivo de registro independiente `transaction_log.log`. La **ruta de archivo** es relativa al contexto de inicio del servidor. A continuación se indica la ruta predeterminada para diferentes servidores:

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

Ejemplo de registro de transacción de ejemplo:
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### Registro de transacciones {#transaction-record-structure-jee}

La estructura del registro de transacciones define cómo se registra cada transacción a través de sus distintos parámetros, como servicio, operación, tipo de transacción y otros. Cada uno se detalla a continuación. La estructura del registro de transacciones es la siguiente:

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **servicio**: nombre del servicio.
* **operación**: nombre de operación.
* **internalService**: Nombre del destinatario de la llamada si hay una llamada interna; de lo contrario, es igual que el nombre del servicio.
* **internalOperation**: El nombre del destinatario de la llamada allí es una llamada interna; de lo contrario, será el mismo que el nombre de la operación.
* **transactionOperationType**: tipo de transacción (enviar, procesar, convertir).
* **transactionCount**: Recuento total de transacciones.
* **elapsedTime**: tiempo entre el inicio de la llamada y la respuesta recibida.
* **transactionDate**: marca de tiempo que indica cuándo se invocó el servicio.

**Registro de transacciones de ejemplo**:

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## Frecuencia de registro de transacciones {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

La frecuencia de registro de transacciones está determinada por las operaciones de actualización en el servidor para cada formulario que se envía, procesa o convierte correctamente.

* En **panel**, el recuento de transacciones se actualiza periódicamente; el valor predeterminado es 1 minuto. Puede actualizar la frecuencia estableciendo la propiedad del sistema en `"com.adobe.idp.dsc.transaction.recordFrequency"`. Por ejemplo, en AEM Forms para JEE en JBoss®, agregue `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` en `JAVA_OPTS` para establecer la frecuencia de actualización en 5 minutos.

* En **registros de transacciones**, la actualización de cada transacción se produce instantáneamente cuando un formulario se envía, procesa o convierte correctamente.

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## Artículos relacionados {#related-articles}

* [Lista de API facturables para AEM Forms en JEE](../../forms/using/transaction-reports-billable-apis-jee.md)
* [Registre una transacción para las API de componentes personalizadas para AEM Forms en JEE](/help/forms/using/record-transaction-custom-component-jee.md)
