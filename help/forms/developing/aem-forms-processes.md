---
title: Explicar los procesos de AEM Forms
description: Descubra cómo los procesos de AEM Forms abarcan la creación, el envío, la gestión de datos, la validación, la integración, la automatización del flujo de trabajo y la administración de resultados.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# Explicar los procesos de AEM Forms {#understanding-aem-forms-processes}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Un caso de uso común es que un conjunto de servicios de AEM Forms funcione en un solo documento. Puede enviar una solicitud al contenedor de servicios creando un proceso con Workbench. Un proceso representa un proceso empresarial que está automatizando. Para obtener información sobre cómo crear procesos, consulte [Usar Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Una vez activado un proceso, se convierte en un servicio y se puede invocar como otros servicios. Una diferencia entre un servicio estándar, como el servicio Encryption y un servicio que se originó a partir de un proceso, es que este último tiene una operación que realiza muchas acciones. Por el contrario, un servicio estándar tiene muchas operaciones. Cada operación suele realizar una acción, como aplicar una directiva a un documento o cifrar un documento.

Los procesos pueden ser de corta o larga duración. Un proceso de corta duración es una operación que se realiza sincrónicamente y en el mismo subproceso de ejecución desde el que se invoca. Las operaciones de corta duración son comparables al comportamiento estándar encontrado en la mayoría de los lenguajes de programación, donde una aplicación cliente llama a un método y espera un valor devuelto.

Sin embargo, hay situaciones en las que un proceso no se puede completar sincrónicamente debido a factores como los siguientes:

* Un proceso puede abarcar una cantidad de tiempo considerable.
* Un proceso puede abarcar límites organizativos.
* Un proceso necesita una entrada externa para que finalice. Por ejemplo, considere una situación en la que un formulario se envíe a un administrador que esté fuera de la oficina. En este caso, el proceso no finaliza hasta que el administrador vuelve y rellena el formulario.

  Estos tipos de procesos se conocen como procesos de larga duración. Se realiza un proceso de larga duración de forma asíncrona, lo que permite que los sistemas interactúen según lo permitan los recursos y permite el seguimiento y la monitorización de la operación. Cuando se invoca un proceso de larga duración, AEM Forms crea un valor de identificador de invocación como parte de un registro que rastrea el estado del proceso de larga duración. El registro se almacena en la base de datos de AEM Forms. Puede depurar registros de procesos de larga duración cuando ya no sean necesarios.

>[!NOTE]
>
>AEM Forms no crea un registro cuando se invoca un proceso de corta duración.

Con el valor del identificador de invocación, puede realizar un seguimiento del estado del proceso de larga duración. Por ejemplo, puede utilizar el valor del identificador de invocación de proceso para realizar operaciones de Process Manager como finalizar una instancia de proceso en ejecución.

**Ejemplo de proceso de corta duración**

La siguiente ilustración es un ejemplo de un proceso de corta duración denominado *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con los ejemplos de código que describen cómo invocar este proceso, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso de corta duración, realiza las siguientes acciones:

1. Obtiene el documento de PDF no protegido que se pasa al proceso como valor de entrada.
1. Cifra el documento de PDF con una contraseña. El nombre del parámetro de entrada para este proceso es `inDoc` y el tipo de datos es document.
1. Guarda el documento de PDF cifrado con contraseña como un archivo PDF en el sistema de archivos local. Este proceso devuelve el documento de PDF cifrado como un valor de salida. El nombre del parámetro de salida para este proceso es `outDoc` y el tipo de datos es document.

   Este proceso se completa sincrónicamente en el mismo subproceso de ejecución desde el que se invocó. El nombre de este proceso de corta duración es `MyApplication/EncryptDocument` y su operación es `invoke`.

   >[!NOTE]
   >
   >Normalmente, un proceso de corta duración consta de más de tres acciones. Puede crear un proceso mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

   *La programación con formularios AEM Forms* describe las siguientes maneras de invocar mediante programación este proceso de corta duración:

   * [Invocación de un proceso de corta duración al pasar un documento no seguro mediante AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (mediante una aplicación de Flex)
   * [Invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (API de invocación de Java™)
   * [Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante datos BLOB a través de HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (ejemplo de servicio web)
   * [Invocar el proceso MyApplication/EncryptDocument mediante REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Ejemplo de proceso de larga duración**

La siguiente ilustración es un ejemplo de un proceso de larga duración.

Este proceso se invoca cuando un solicitante envía un formulario de préstamo. El proceso no finaliza hasta que un responsable de préstamo aprueba o rechaza la solicitud de préstamo. El nombre de este proceso de larga duración es *FirstAppSolution/PreLoanProcess* y su operación es `invoke_Async`. Este proceso debe invocarse asincrónicamente. Para obtener información acerca de cómo invocar mediante programación este proceso de larga duración, vea [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Este proceso se puede crear siguiendo el tutorial especificado en [Creación de la primera aplicación de AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
