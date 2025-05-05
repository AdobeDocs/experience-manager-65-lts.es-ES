---
title: Flujo de trabajo centrado en Forms en OSGi
description: Utilice el flujo de trabajo de AEM Forms para automatizar y generar rápidamente revisiones y aprobaciones, para iniciar servicios de documento
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3667'
ht-degree: 95%

---

# Flujo de trabajo centrado en Forms en OSGi{#forms-centric-workflow-on-osgi}

![imagen a pantalla completa](do-not-localize/header.png)

Las empresas recopilan datos de cientos y miles de formularios, varios sistemas back-end y fuentes de datos en línea o sin conexión. También tienen un conjunto dinámico de usuarios para tomar decisiones sobre los datos, lo que implica procesos de revisión y aprobación iterativos.

Junto con los flujos de trabajo de revisión y aprobación para audiencias internas y externas, las organizaciones y empresas grandes tienen tareas repetitivas. Por ejemplo, convertir un documento PDF a otro formato. Cuando se realizan manualmente, estas tareas consumen mucho tiempo y recursos. Las empresas también tienen requisitos legales para firmar digitalmente un documento y archivar datos de formulario para su uso posterior en formatos predefinidos.

## Introducción al flujo de trabajo centrado en Forms en OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puede utilizar flujos de trabajo de AEM para generar rápidamente flujos de trabajo adaptables basados en Forms. Estos flujos de trabajo se pueden utilizar para revisiones y aprobaciones, flujos de procesos empresariales, para iniciar servicios de documento, integrarse con el flujo de trabajo de firmas de Adobe Sign y operaciones similares. Por ejemplo, en el procesamiento de la solicitud de tarjeta de crédito, el empleado deja los flujos de trabajo de aprobación y guarda un formulario como documento de PDF. Además, estos flujos de trabajo se pueden utilizar dentro de una organización o entre firewall de redes.

Con el flujo de trabajo centrado en formularios en OSGi, puede generar e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la funcionalidad de administración de procesos completa en la pila JEE. El desarrollo y la administración de flujos de trabajo utilizan las funciones conocidas de los flujo de trabajo de AEM y la bandeja de entrada AEM. Los flujos de trabajo forman la base de la automatización de los procesos empresariales en el mundo real que abarcan varios sistemas de software, redes, departamentos e incluso organizaciones.

Una vez configurados, estos flujos de trabajo se pueden habilitar manualmente para completar un proceso definido o ejecutarse programáticamente cuando los usuarios envíen un formulario o cartas de[ Administración de correspondencia](/help/forms/using/cm-overview.md). Con estas funciones mejoradas del flujo de trabajo de AEM, AEM Forms ofrece dos funciones distintas, aunque similares. Como parte de su estrategia de implementación, debe decidir cuál funciona para usted. Consulte una [comparación](capabilities-osgi-jee-workflows.md) de los flujos de trabajo de AEM centrados en Forms en OSGi y Process Management en JEE. Además, para la topología de implementación, consulte, [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

El flujo de trabajo centrado en Forms en OSGi amplía [la bandeja de entrada de AEM](/help/sites-authoring/inbox.md) y proporciona componentes adicionales (pasos) para el editor de flujos de trabajo de AEM para agregar compatibilidad con flujos de trabajo centrados en AEM Forms. La bandeja de entrada extendida de AEM tiene funcionalidades similares a las de [AEM Forms Workspace](introduction-html-workspace.md). Junto con la administración de flujos de trabajo centrados en las personas (aprobación, revisión, etc.), puede utilizar flujos de trabajo de AEM para automatizar operaciones de trabajo relacionadas con [servicios de documentos](/help/sites-developing/workflows-step-ref.md) (por ejemplo, generar PDF) y documentos de firma electrónica (Adobe Sign).

Todos los pasos del flujo de trabajo de AEM Forms admiten el uso de variables. Las variables permiten realizar pasos en el flujo de trabajo para mantener y pasar metadatos por varios pasos durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. También puede crear colecciones de variables (matriz) para almacenar varias instancias de datos relacionados y del mismo tipo. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en base al valor que mantiene o para almacenar información que se necesite más adelante en un proceso. Para obtener más información sobre el uso de variables en estos componentes (pasos) del flujo de trabajo centrados en Forms, consulte [Flujo de trabajo centrado en Forms en OSGi: pasos de referencia](../../forms/using/aem-forms-workflow-step-reference.md). Para obtener información sobre la creación y la administración de variables, consulte [Variables en flujos de trabajo de AEM](../../forms/using/variable-in-aem-workflows.md).

En el siguiente diagrama se describe el procedimiento de extremo a extremo para crear, ejecutar y monitorizar un flujo de trabajo centrado en Forms en OSGi.

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de comenzar {#before-you-start}

* Un flujo de trabajo es una representación de un proceso empresarial real. Tenga preparados su proceso empresarial real y la lista de los participantes del proceso. Además, prepare el material colateral (formularios adaptables, documentos PDF, etc.) antes de empezar a crear un flujo de trabajo.
* Un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM y ayudan a informar sobre el progreso del flujo de trabajo. Divida el proceso empresarial en fases lógicas.
* Puede configurar el paso Asignar tarea del flujo de trabajo de AEM para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. [habilita las notificaciones por correo electrónico](#configure-email-service).
* Un flujo de trabajo también puede utilizar Adobe Sign para las firmas digitales. Si planea utilizar Adobe Sign en un flujo de trabajo, configure [Adobe Sign para AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) antes de utilizarlo en un flujo de trabajo.

## Cree un modelo del flujo de trabajo {#create-a-workflow-model}

Un modelo del flujo de trabajo consiste en la lógica y el flujo de un proceso empresarial. Se compone de una serie de pasos. Estos pasos son componentes de AEM. Puede ampliar los pasos del flujo de trabajo con parámetros y scripts para proporcionar más funcionalidad y control, según sea necesario. AEM Forms proporciona algunos pasos además de pasos de AEM disponibles de forma predeterminada. Para obtener una lista detallada de AEM Forms y de sus pasos, consulte [Pasos de referencia del flujo de trabajo de AEM](/help/sites-developing/workflows-step-ref.md) y [Flujo de trabajo centrado en Forms en OSGi: pasos de referencia](../../forms/using/aem-forms-workflow.md).

AEM proporciona una interfaz de usuario intuitiva para crear un modelo del flujo de trabajo siguiendo los pasos proporcionados. Para obtener instrucciones paso a paso para crear un modelo del flujo de trabajo, consulte [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md). El siguiente ejemplo proporciona instrucciones paso a paso para crear un modelo del flujo de trabajo para un flujo de trabajo de aprobación y revisión:

>[!NOTE]
>
>Debe ser miembro del grupo de editor del flujo de trabajo para crear o editar un modelo del flujo de trabajo.

### Creación de un modelo para un flujo de trabajo de aprobación y revisión {#create-a-model-for-an-approval-and-review-workflow}

El flujo de trabajo de aprobación y revisión corresponde a las tareas que requieren intervención humana para tomar decisiones. En el siguiente ejemplo se crea un modelo del flujo de trabajo para una solicitud de préstamo hipotecario que debe rellenar un agente bancario de la oficina principal. Una vez completada la solicitud, se envía para su aprobación. Posteriormente, la solicitud aprobada se envía al solicitante para que la firme mediante Adobe Sign.

A continuación, puede encontrar el ejemplo como paquete adjunto. Importe e instale el ejemplo mediante el administrador de paquetes. También puede realizar los siguientes pasos para crear manualmente el modelo del flujo de trabajo para la solicitud:

En el ejemplo se crea un modelo del flujo de trabajo con una solicitud hipotecaria que rellenará un agente bancario de la oficina principal. Una vez completada, la solicitud se envía para su aprobación. Posteriormente, la solicitud aprobada se envía al cliente para que la firme mediante Adobe Sign. Puede importar e instalar el ejemplo mediante el administrador de paquetes.

[Obtener archivo](assets/example-mortgage-loan-application.zip)

1. Abra la consola Modelos de flujo de trabajo. La URL predeterminada es `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Seleccione **Crear** y, a continuación, **Crear modelo**. Aparecerá el cuadro de diálogo Agregar modelo del flujo de trabajo.
1. Escriba el **Título** y el **Nombre** (opcional). Por ejemplo, una solicitud hipotecaria. Seleccione **Listo**.
1. Seleccione el modelo de flujo de trabajo recién creado y seleccione **Editar**. Ahora puede agregar pasos al flujo de trabajo para crear lógica empresarial. La primera vez que cree un modelo del flujo de trabajo, contendrá:

   * Los pasos: Inicio del flujo y Fin del flujo. Estos pasos representan el principio y el final del flujo de trabajo. Estos pasos son obligatorios y no se pueden editar ni eliminar.
   * Un ejemplo de paso de participante denominado Paso 1. Este paso está configurado para asignar un elemento de trabajo al administrador. Elimine este paso.

1. Habilitar las notificaciones por correo electrónico. Puede configurar el flujo de trabajo centrado en Forms en OSGi para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Realice las siguientes configuraciones para habilitar las notificaciones por correo electrónico:

   1. Vaya al administrador de configuración de AEM en `https://[server]:[port]/system/console/configMgr`.
   1. Abra la configuración de **[!UICONTROL Day CQ Mail Service]**. Especifique un valor para el **[!UICONTROL nombre del host del servidor SMTP]**, **[!UICONTROL el puerto del servidor SMTP]** y **[!UICONTROL los campos de la dirección “Desde”]**. Haga clic en **[!UICONTROL Guardar]**.
   1. Abra la configuración de **[!UICONTROL Day CQ Link Externalizer]**. En el campo **[!UICONTROL Dominios]** especifique el nombre del host o la dirección IP real y el número de puerto para las instancias locales, Autor y Publicación. Haga clic en **[!UICONTROL Guardar]**.

1. Crear fases del flujo de trabajo. Un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM y en el progreso del informe del flujo de trabajo.

   Para definir una fase, seleccione el icono de ![info-circle](assets/info-circle.png) para abrir las propiedades del modelo del flujo de trabajo, abra la pestaña **Fases**, agregue fases para el modelo del flujo de trabajo y seleccione **Guardar y cerrar**. Para la solicitud de hipoteca de ejemplo, cree fases: solicitud del préstamo, estado de la solicitud del préstamo, documentos a firmar y documento del préstamo firmado.

1. Arrastre y suelte el explorador de fases **Asignar tarea** al modelo del flujo de trabajo. Conviértalo en el primer paso del modelo.

   El componente Asignar tarea asigna la tarea que ha creado el flujo de trabajo, a un usuario o grupo. Además de asignar la tarea, puede utilizar el componente para especificar un formulario adaptable o un PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar los datos que han introducido los usuarios y un PDF no interactivo o un formulario adaptable de solo lectura solo se utiliza para revisar los flujos de trabajo.

   También puede utilizar el paso para controlar el comportamiento de la tarea. Por ejemplo, al crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, la ruta de los datos enviados, la ruta de los datos que se van a rellenar previamente y las acciones predeterminadas. Para obtener información detallada sobre las opciones del paso Asignar tarea, consulte el documento [Flujo de trabajo centrado en Forms en OSGi: pasos de referencia](../../forms/using/aem-forms-workflow.md).

   ![workflow-editor](assets/workflow-editor.png)

   Para el ejemplo de la solicitud de la hipoteca, configure el paso Asignar tarea para utilizar un formulario adaptable de solo lectura y mostrar el documento PDF una vez que se haya completado la tarea. Además, seleccione el grupo de usuarios autorizado para aprobar la solicitud del préstamo. En la pestaña **Acciones**, deshabilite la opción **Enviar**. Cree una variable **actionTaken** del tipo de datos String y especifíquela como **Variable de ruta**. Por ejemplo, actionTaken. Además, agregue las rutas Aprobar y Rechazar. Las rutas se muestran como acciones independientes (botones) en la bandeja de entrada AEM. El flujo de trabajo selecciona una rama en función de la acción (botón) que pulse un usuario.

   Puede importar el paquete de ejemplo, que está disponible para descargar al principio de la sección, para el conjunto completo de valores de todos los campos del paso Asignar tarea configurado, para el ejemplo de solicitud de hipoteca.

1. Arrastre y suelte el componente OR Split desde el explorador de pasos al modelo del flujo de trabajo. OR Splits crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en su flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

   Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, un script ECMA o un script externo.

   Utilice el editor de expresiones para crear expresiones de enrutamiento para las ramas 1 y 2. Estas expresiones de enrutamiento ayudan a elegir una rama en base a la acción del usuario en la bandeja de entrada AEM.

   **Expresión de enrutamiento para la rama 1**

   Cuando el usuario pulse **Aprobar** en la bandeja de entrada AEM, se activará la rama 1.

   ![Ejemplo de OR Split](assets/orsplit_branch1_active_new.png)

   **Expresión de enrutamiento para la rama 2**

   Cuando el usuario pulse **Rechazar** en la bandeja de entrada AEM, se activará la rama 2.

   ![Ejemplo de OR Split](assets/orsplit_branch2_active_new.png)

   Para obtener información sobre la creación de expresiones de enrutamiento mediante variables, consulte [Variables en flujos de trabajo de AEM Forms](../../forms/using/variable-in-aem-workflows.md).

1. Agregue otros pasos del flujo de trabajo para crear la lógica empresarial.

   Para el ejemplo de la hipoteca, agregue un documento de registro generado, dos pasos de la asignación de tareas y un paso del documento de firma a la rama 1 del modelo, como se muestra en la siguiente imagen. Un paso de la asignación de tareas es mostrar y enviar **documentos de préstamo a firmar al solicitante** y otro componente de asignación de tareas es **mostrar documentos firmados**. Además, agregue un componente de la asignación de tareas a la rama 2. Se activará cuando un usuario pulse Rechazar en la bandeja de entrada AEM.

   Para obtener el conjunto completo de valores de todos los campos de los pasos de la asignación de tareas, el paso Documento de registro y el de documento de firma configurado, por ejemplo, la solicitud de hipoteca, importe el paquete de ejemplo, disponible para descargar al principio de esta sección.

   El modelo del flujo de trabajo está listo. Puede iniciar el flujo de trabajo mediante varios métodos. Para obtener más información, consulte [Iniciar un flujo de trabajo centrado en Forms en OSGi](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## Crear una solicitud de flujo de trabajo centrada en formularios  {#create-a-forms-centric-workflow-application}

La solicitud es el formulario adaptable asociado al flujo de trabajo. Cuando una solicitud se envía a través de la bandeja de entrada, inicia el flujo de trabajo asociado. Para que un flujo de trabajo de Forms esté disponible como solicitud en la bandeja de entrada de AEM y la aplicación de AEM Forms, haga lo siguiente para crear una solicitud del flujo de trabajo:

>[!NOTE]
>
>Debe ser miembro del grupo fd-administrator para poder crear y administrar solicitudes de flujo de trabajo.

1. En la instancia de Autor de AEM, vaya a ![herramientas-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Administrar solicitud de flujo de trabajo]** y pulse **[!UICONTROL Crear]**.
1. En la ventana Crear solicitud de flujo de trabajo, introduzca entradas para los siguientes campos y pulse **Crear**. Se creará una solicitud nueva que aparecerá en la pantalla Solicitudes de flujo de trabajo.

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>El título se ve en la bandeja de entrada AEM y ayuda a los usuarios a elegir una solicitud. Haga que siga siendo descriptivo. Por ejemplo, la solicitud de apertura de una cuenta de ahorros.<br /> </td>
  </tr>
  <tr>
   <td>Nombre </td>
   <td>Especifique el nombre de la solicitud. Todos los caracteres que no sean letras, números, guiones o guiones bajos se sustituirán por guiones. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>La descripción es visible en la bandeja de entrada AEM. Proporcione información detallada sobre la solicitud en los campos de descripción. Por ejemplo, Finalidad de la solicitud.<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td><p>Especifique la ruta de un formulario adaptable. Cuando un usuario inicia una solicitud, se muestra el formulario adaptable especificado.</p> <p><strong>Nota</strong>: Las solicitudes de flujo de trabajo no admiten formularios ni documentos PDF que tengan más de una página o que requieran desplazamiento en Apple iPad. Cuando se abre una solicitud en Apple iPad y el formulario adaptable o el documento PDF es más largo que una página, se pierden los campos y el contenido del formulario de la segunda página.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acceso</td>
   <td><p>Seleccionar un grupo. La solicitud solo es visible en la bandeja de entrada AEM para los miembros del grupo seleccionado. La opción de grupo de acceso hace que todos los grupos del grupo del flujo de trabajo de usuarios estén disponibles para seleccionarlos. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servicio de rellenado previo</td>
   <td>Seleccione un <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servicio de rellenado previo</a> para el formulario adaptable.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de flujo de trabajo</td>
   <td>Seleccione un <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">modelo de flujo de trabajo</a> para la solicitud. Un modelo de flujo de trabajo consiste en la lógica y el flujo del proceso empresarial. </td>
  </tr>
  <tr>
   <td>Ruta del archivo de datos</td>
   <td>Especifique la ruta del archivo de datos en el repositorio crx. La ruta es relativa a la carga útil del formulario adaptable y contiene el nombre del archivo de datos. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Ruta de archivos adjuntos</td>
   <td>Especifique la ruta de la carpeta de archivos adjuntos en el repositorio crx. La ruta de acceso de datos adjuntos es relativa a la ubicación de carga útil. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Documento de ruta de registro</td>
   <td>Especifique la ruta del archivo Documento de registro en el repositorio crx. La ruta es relativa a la ubicación de carga útil del formulario adaptable. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar un flujo de trabajo centrado en Forms en OSGi {#launch}

Puede iniciar o habilitar un flujo de trabajo centrado en Forms mediante:

* [El envío de una solicitud desde la bandeja de entrada AEM](#inbox)
* [El envío de una aplicación desde la aplicación de AEM Forms](#afa)

* [Enviar un formulario adaptable](#af)
* [Usar una carpeta inspeccionada](#watched)

* [El envío de una comunicación interactiva o una carta](#letter)

### El envío de una solicitud desde la bandeja de entrada AEM {#inbox}

La solicitud de flujo de trabajo que ha creado está disponible como solicitud en la bandeja de entrada. Los usuarios que sean miembros del grupo del flujo de trabajo de usuarios pueden rellenar y enviar la solicitud que activa el flujo de trabajo asociado. Para obtener información sobre el uso de la bandeja de entrada de AEM para enviar solicitudes y administrar tareas, consulte [Administrar solicitudes y tareas de Forms en la bandeja de entrada de AEM](../../forms/using/manage-applications-inbox.md).

### Enviar una aplicación desde la aplicación de AEM Forms {#afa}

La aplicación de AEM Forms se sincroniza con un servidor de AEM Forms y le permite cambiar los datos del formulario, las tareas, las aplicaciones de flujo de trabajo y la información guardada (borradores/plantillas) en su cuenta. Para obtener más información, consulte [aplicación de AEM Forms](/help/forms/using/aem-forms-app.md) y artículos relacionados.

### Enviar un formulario adaptable {#af}

Puede configurar las acciones de envío de un formulario adaptable para iniciar un flujo de trabajo al enviar el formulario adaptable. Los formularios adaptables proporcionan la acción de envío **Invocar un flujo de trabajo de AEM** para iniciar un flujo de trabajo al enviar un formulario adaptable. Para obtener información detallada sobre la acción de envío, consulte [Configurar la acción de envío](../../forms/using/configuring-submit-actions.md). Para enviar un formulario adaptable a través de la aplicación de AEM Forms, habilite Sincronizar con la aplicación de AEM Forms en las propiedades del formulario adaptable.

Puede configurar un formulario adaptable para sincronizar, enviar y habilitar un flujo de trabajo desde la aplicación de AEM Forms. Para obtener más información, consulte [trabajar con un formulario](/help/forms/using/working-with-form.md).

### Usar una carpeta vigilada {#watched}

Un administrador (un miembro del grupo de administradores de fd) puede configurar una carpeta de red para ejecutar un flujo de trabajo preconfigurado cuando un usuario coloca un archivo (como un archivo PDF) en la carpeta. Una vez finalizado el flujo de trabajo, puede guardar el archivo resultante en una carpeta de salida especificada. Esta carpeta se conoce como [Carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md). Realice el siguiente procedimiento para configurar una carpeta vigilada para iniciar un flujo de trabajo:

1. En la instancia de autor de AEM, vaya a ![herramientas-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configurar carpeta vigilada]**. Se mostrará una lista de las carpetas vigiladas ya configuradas.
1. Seleccione **[!UICONTROL Nuevo]**. Se mostrará una lista de campos. Especifique un valor para los siguientes campos para configurar una carpeta vigilada para un flujo de trabajo:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Nombre</code></td>
   <td>Especifique el nombre de la carpeta vigilada. Este campo solo admite caracteres alfanuméricos.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Ruta </code></td>
   <td>Especifique la ubicación física de la carpeta vigilada. En un entorno agrupado, utilice una carpeta de red compartida a la que se pueda acceder desde el nodo de clúster de AEM.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Procesar archivos mediante</code></td>
   <td>Seleccionar el <span class="uicontrol">flujo de trabajo </code>JVM. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modelo de flujo de trabajo</code></td>
   <td>Seleccione un modelo de flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Patrón de archivo de salida</code></td>
   <td>Especifique la estructura de directorios para los archivos y directorios de salida. También puede especificar un patrón <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">para archivos y directorios de salida</a>.</td>
  </tr>
 </tbody>
</table>

1. Seleccione **Avanzado**. Especifique un valor para el siguiente campo y pulse **Crear**. La carpeta vigilada está configurada para iniciar un flujo de trabajo. Ahora, cada vez que se coloque un archivo en el directorio de entrada de la carpeta vigilada, se activará el flujo de trabajo especificado.

   | Campo | Descripción |
   |---|---|
   | Filtro de asignador de cargas útiles | Cuando se cree una carpeta vigilada, se creará una estructura de carpetas en el repositorio crx. La estructura de carpetas puede servir como carga útil para el flujo de trabajo. Puede escribir un script para asignar un flujo de trabajo de AEM y aceptar entradas de la estructura de carpetas vigilada. Una implementación predeterminada está disponible y se enumera en el filtro asignador de cargas útiles. Si no tiene una implementación personalizada, seleccione la implementación predeterminada. |

   La pestaña Avanzado contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Para obtener más información sobre todos los campos, consulte el artículo [Crear o configurar una carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

### Enviar una comunicación interactiva o una carta {#letter}

Puede asociar y ejecutar un flujo de trabajo centrado en Forms en OSGi al enviar una comunicación interactiva o una carta. En Administración de correspondencia, los flujos de trabajo se utilizan para las cartas y las comunicaciones interactivas posteriores al procesamiento. Por ejemplo, enviar por correo electrónico, imprimir, enviar por fax o archivar cartas finales. Para ver los pasos detallados, consulte [Procesamiento posterior de comunicaciones interactivas y cartas](../../forms/using/submit-letter-topostprocess.md).

## Configuraciones adicionales {#additional-configurations}

### Configurar el servicio de correo electrónico {#configure-email-service}

Puede utilizar los pasos Asignar tarea y Enviar correo electrónico de flujos de trabajo de AEM para enviar un correo electrónico. Realice los siguientes pasos para especificar los servidores de correo electrónico y otras configuraciones necesarias para enviar correo electrónico:

1. Vaya al administrador de configuración de AEM en `https://[server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Day CQ Mail Service]**. Especifique un valor para el **[!UICONTROL nombre del host del servidor SMTP]**, **[!UICONTROL el puerto del servidor SMTP]** y **[!UICONTROL los campos de la dirección “Desde”]**. Haga clic en **[!UICONTROL Guardar]**.
1. Abra la configuración de **[!UICONTROL Day CQ Link Externalizer]**. En el campo **[!UICONTROL Dominios]** especifique el nombre del host o la dirección IP real y el número de puerto para las instancias locales, Autor y Publicación. Haga clic en **[!UICONTROL Guardar]**.

### Purgar instancias del flujo de trabajo {#purge-workflow-instances}

Al minimizar el número de instancias del flujo de trabajo, aumenta el rendimiento del motor de flujos de trabajo, por lo que puede depurar con regularidad las instancias del flujo de trabajo completadas o en ejecución desde el repositorio. Para obtener información detallada, consulte [Depuración regular de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md#regular) depuración de instancias de flujo de trabajo.

## Parametrizar datos confidenciales a variables de flujo de trabajo y almacenarlos en repositorios de datos externos {#externalize-wf-variables}

Cualquier dato enviado desde formularios adaptables a flujos de trabajo [!DNL Experience Manager]pueden tener PII (información de identificación personal) o SPD (datos personales confidenciales) de los usuarios finales de su empresa. Sin embargo, no es obligatorio almacenar los datos almacenados en el [!DNL Adobe Experience Manager] [Repositorio JCR](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html?lang=es). Puede externalizar el almacenamiento de datos del usuario final en el almacenamiento de datos administrado (por ejemplo, el almacenamiento del blob de Azure) al parametrizar la información en [variables de flujo de trabajo](/help/forms/using/variable-in-aem-workflows.md).

En un [!DNL Adobe Experience Manager] flujo de trabajo de Forms, los datos se procesan y pasan a través de una serie de pasos de flujo de trabajo mediante variables de flujo de trabajo. Estas variables se denominan propiedades o pares clave-valor que se almacenan en el nodo de metadatos de instancias de flujo de trabajo; por ejemplo, `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. Estas variables de flujo de trabajo se pueden externalizar en un repositorio independiente que no sea JCR y luego procesar mediante [!DNL Adobe Experience Manager] flujos de trabajo. [!DNL Adobe Experience Manager] proporciona API `[!UICONTROL UserMetaDataPersistenceProvider]` para almacenar las variables de flujo de trabajo en el almacenamiento externo administrado. Para obtener más información sobre el uso de variables de flujo de trabajo para repositorios de datos de propiedad del cliente en [!DNL Adobe Experience Manager], consulte [Administrar variables de flujo de trabajo para repositorios de datos externos](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] proporciona el siguiente [ejemplo](https://github.com/adobe/workflow-variable-externalizer) para almacenar variables desde el mapa de metadatos del flujo de trabajo al almacenamiento del blob de Azure, con la API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). En líneas similares, puede utilizar el ejemplo como guía para utilizar la API [UserMetaDataPersistenceProvider] para externalizar las variables de flujo de trabajo en cualquier otro almacenamiento de datos externo a [!DNL Adobe Experience Manager] y administrar lo mismo.

>[!NOTE]
>
>Cuando almacene las variables de flujo de trabajo en un almacenamiento de datos externo, consulte los indicadores en las [directrices para flujos de trabajo de almacenamiento de datos externos](#guidelines-workflows-external-data-storage).

### Instalar la implementación de muestra de la API del flujo de trabajo

Para almacenar variables de flujo de trabajo en el almacenamiento del blob de Azure administrado, haga lo siguiente:
1. Instale el [ejemplo](https://github.com/adobe/workflow-variable-externalizer) API de flujo de trabajo [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) de la siguiente manera:

   1. Ejecute en el directorio raíz del proyecto el comando `mvn clean install` con Maven 3.

   1. Para implementar el paquete y el paquete de contenido para su creación, ejecute `mvn clean install -PautoInstallPackage`.

   1. Para implementar solo el paquete en autor, ejecute `mvn clean install -PautoInstallBundle`.

1. Inicialice las siguientes propiedades en el archivo de configuración OSGi del externalizador en el paquete de contenido `ui.config`:

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

Los siguientes son los propósitos (y ejemplos) de estas propiedades:

* **accountKey** es la clave secreta para autorizar el acceso.

* **accountName** es la cuenta de Azure en la que se deben almacenar los datos.

* **endpointSuffix**, por ejemplo, `core.windows.net`.

* **containerName** es el contenedor de la cuenta donde se deben almacenar los datos. El ejemplo supone que el contenedor existe.

* **protocolo**, por ejemplo, `https` o `http`.

1. Configure el modelo de flujo de trabajo en [!DNL Adobe Experience Manager]. Para saber cómo configurar el modelo de flujo de trabajo para un almacenamiento externo, consulte [Configurar el modelo de flujo de trabajo](#configure-aem-wf-model).

### Configurar el modelo de flujo de trabajo en [!DNL Adobe Experience Manager] para el almacenamiento de datos externos {#configure-aem-wf-model}

Para configurar un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo haga lo siguiente:

1. Navegue hasta **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. Seleccione el nombre de un modelo y pulse **[!UICONTROL Editar]**.

1. Seleccione el icono Información de página y luego pulse **[!UICONTROL Abrir propiedades]**.

1. Seleccione **[!UICONTROL Externalizar el almacenamiento de los datos del flujo de trabajo]**.

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar las propiedades.

### Directrices para los flujos de trabajo de AEM de un almacenamiento de datos externo {#guidelines-workflows-external-data-storage}

Estas son las directrices a seguir a la hora de usar flujos de trabajo de [!DNL Adobe Experience Manager] y almacenar datos en almacenes de datos externos (por ejemplo, el servidor de almacenamiento de Microsoft Azure):

* Utilice variables para almacenar los datos al definir los archivos de datos de entrada y salida y los archivos adjuntos en los pasos del modelo de flujo de trabajo. No seleccione las opciones **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]**. Las opciones **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]** no se mostrarán automáticamente una vez que [ [!DNL Adobe Experience Manager] haya configurado un modelo de flujo de trabajo de para un almacenamiento de datos externo](#configure-aem-wf-model).

* Utilice variables para almacenar los archivos de datos y los archivos adjuntos cuando envíe un formulario adaptable a un flujo de trabajo de AEM. No seleccione la opción **[!UICONTROL Relativo a carga útil]** cuando envíe un formulario adaptable a un [!DNL Adobe Experience Manager]flujo de trabajo La opción **[!UICONTROL Relativo a carga útil]** no se mostrará automáticamente una vez que [ [!DNL Adobe Experience Manager] haya configurado un modelo de flujo de trabajo de para un almacenamiento de datos externo](#configure-aem-wf-model).

* No utilice un paso de un flujo de trabajo de personalizado [!DNL Adobe Experience Manager]de un modelo de flujos de trabajo para almacenar datos en el [!UICONTROL repositorio CRX DE].

* Cuando [configure un  [!DNL Adobe Experience Manager]  modelo de flujo de trabajo de para un almacenamiento de datos externo](#configure-aem-wf-model), no cree columnas personalizadas para la [!DNL Adobe Experience Manager]bandeja de entrada[!UICONTROL , &#x200B;]ya que los valores de las columnas personalizadas no se recuperan si el elemento de trabajo [!DNL Adobe Experience Manager] de la [!UICONTROL bandeja de entrada &#x200B;]pertenece a un flujo de trabajo marcado para un almacenamiento externo.
