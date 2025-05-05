---
title: Ver y comprender los informes de transacciones
description: Utilizar los informes de transacciones para tomar una decisión informada sobre el uso del producto y las inversiones de reequilibrio en hardware y software.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 93%

---

# Ver y comprender los informes de transacciones de AEM Forms en OSGi{#viewing-and-understanding-transaction-reports}

Los informes de transacciones permiten capturar y realizar un seguimiento de la cantidad de formularios enviados, documentos procesados y documentos representados. El objetivo detrás del seguimiento de estas transacciones es tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software. Para obtener más información, consulte [Información general sobre los informes de transacciones de AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configurar informes de transacciones  {#setting-up-transaction-reports}

La función de informes de transacciones está disponible como parte del paquete de complementos de AEM Forms. Para obtener información sobre la instalación del paquete de complementos en todas las instancias de autor y publicación, consulte [Instalar y configurar AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Una vez que tenga instalado el paquete de complementos de AEM Forms, haga lo siguiente:

* Habilite la replicación inversa en todas las instancias de publicación
* Habilite los informes de transacciones
* Proporcione derechos para ver un informe de transacciones
* (Opcional) Configure el período de vaciado de transacción y las bandejas de salida [&#128279;](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Los informes de transacciones de AEM Forms no admiten topologías que contengan solo instancias de publicación.
>* Antes de usar informes de transacciones, asegúrese de que la replicación inversa esté habilitada para todas las instancias de publicación.
>* Los datos de transacción se replican de forma inversa de una instancia de publicación a la instancia de autor o procesamiento correspondiente. El autor o la instancia de procesamiento no pueden replicar más datos en otra instancia.
>

### Habilite la replicación inversa en todas las instancias de publicación {#enable-reverse-replication-on-all-the-publish-instances}

Los informes de transacciones utilizan la replicación inversa para consolidar el recuento de transacciones desde instancias de publicación hasta instancias de autor. Configurar la replicación inversa en todas las instancias de publicación. Para obtener instrucciones detalladas sobre la configuración de la replicación inversa, consulte [replicación](/help/sites-deploying/replication.md).

### Habilite los informes de transacciones {#enable-transaction-reports}

Los informes de transacciones están deshabilitados de forma predeterminada. Los informes se pueden habilitar desde la consola web de AEM. Para habilitar los informes de transacciones en un entorno de AEM Forms, realice los siguientes pasos en todas las instancias de autor y publicación:

1. Inicie sesión en una instancia de AEM como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola web**.
1. Localice y abra el servicio **Informes de transacciones de Forms**.
1. Seleccione la casilla de verificación Registrar transacciones. Haga clic en **Guardar**.

   Repita los pasos 1-3 en todas las instancias de autor y publicación.

### Proporcione derechos para ver un informe de transacciones {#provide-rights-to-view-a-transaction-report}

Solo los miembros del grupo fd-administrator pueden ver los informes de transacciones. Para permitir que un usuario vea informes de transacciones, haga que los usuarios sean miembros del grupo fd-administrator. Para obtener instrucciones sobre cómo hacer que un usuario sea miembro de un grupo de AEM, consulte [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md).

### (Opcional) Configurar el período de vaciado de transacción y las bandejas de salida {#optional-configure-transaction-flush-period-and-outboxes}

Las transacciones se almacenan en caché antes de almacenarse en el repositorio. Se sigue el proceso para garantizar que no haya escrituras frecuentes en el repositorio. De forma predeterminada, el período de almacenamiento en caché (Período de vaciado de transacción) está establecido en 60 segundos. Puede cambiar el período predeterminado para adaptarlo a su entorno. Realice los siguientes pasos para cambiar el período de almacenamiento en caché predeterminado:

1. Inicie sesión en las instancias de autor como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola web**.
1. Busque y abra el servicio **Proveedor de almacenamiento del repositorio de transacciones de Forms**.
1. Especifique el número de segundos en el campo **Período de vaciado de transacción**. Haga clic en **Guardar**.

La replicación inversa copia los datos de transacción en la bandeja de salida predeterminada de las instancias de autor. Puede colocar los datos de transacción en una bandeja de salida personalizada. Siga estos pasos para especificar una bandeja de salida personalizada:

1. Inicie sesión en las instancias de autor como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola web**.
1. Busque y abra el servicio **Proveedor de almacenamiento del repositorio de transacciones de Forms**.
1. Especifique el nombre de la bandeja de salida personalizada en el campo **Bandejas de salida**. Haga clic en **Guardar**. Se crea una bandeja de salida con el nombre especificado en todas las instancias de autor.

## Ver el informe de transacciones {#viewing-the-transaction-report}

Puede ver informes de transacciones sobre instancias de autor o publicación. El informe de transacción de la instancia de autor proporciona una suma agregada de todas las transacciones que se realizan en las instancias de autor y publicación configuradas. El informe de transacciones de la instancia de publicación ofrece un recuento de transacciones que se realizan solamente en la instancia de publicación subyacente. Siga estos pasos para ver el informe:

1. Inicie sesión en el servidor de AEM Forms en `https://[hostname]:'port'`.
1. Vaya a **Herramientas** > **Formularios** > **Ver informe de transacciones**.

## Comprender el informe {#understanding-the-report}

AEM Forms muestra los informes de transacciones desde la fecha configurada, como se muestra en el siguiente informe de resumen:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilice la opción **Restablecer la fecha a hoy** para restablecer los registros de transacción. Cuando restablece la fecha a hoy, se pierden todos los registros de transacción anteriores. Cuando restablece la fecha en una instancia de autor, el cambio no afecta a los informes de transacción en las instancias de publicación y a la inversa.
* Utilice **Mostrar transacciones de solo instancias de publicación** para ver todas las transacciones que se produjeron únicamente en la instancia de publicación o en la granja de publicación configurada.
* Utilice las categorías: **Documento procesado**, **Documentos representados** y **Formularios enviados** para ver las transacciones correspondientes. Para el tipo de transacciones contabilizadas en estas categorías, consulte [API facturables de informes de transacciones](../../forms/using/transaction-reports-billable-apis.md).

## Ver registros de informes de transacciones {#view-transaction-reporting-logs}

Los informes de transacciones colocan toda la información mostrada en el informe y cierta información adicional en los registros. La información proporcionada en los registros es útil para los usuarios avanzados. Por ejemplo, los registros dividen las transacciones en varias categorías granulares en comparación con tres categorías consolidadas mostradas en el informe. Los registros están disponibles en el archivo `error.log` en el directorio `/crx-repository/logs/`. Los registros están disponibles aunque no habilite los informes de transacción desde la consola web de AEM.

## Artículos relacionados {#related-articles}

* [Información general de informes de transacciones para AEM Forms en OSGi](../../forms/using/transaction-reports-overview.md)
* [API facturables de informes de transacciones para AEM Forms en OSGi](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar una transacción para implementaciones personalizadas para AEM Forms en OSGi](/help/forms/using/record-transaction-custom-implementation.md)
