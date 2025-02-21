---
title: Supervisión de recursos del servidor mediante la consola JMX
description: Obtenga información sobre cómo monitorizar los recursos del servidor mediante la consola JMX.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Operations
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '4830'
ht-degree: 0%

---

# Supervisión de recursos del servidor mediante la consola JMX{#monitoring-server-resources-using-the-jmx-console}

La consola JMX permite supervisar y administrar los servicios en el servidor de CRX. Las secciones siguientes resumen los atributos y las operaciones expuestos a través del marco de trabajo JMX.

Para obtener información acerca de cómo usar los controles de la consola, vea [Usar la consola JMX](#using-the-jmx-console). Para obtener información básica sobre JMX, consulte la página [Java Management Extensions (JMX) Technology](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) en el sitio web de Oracle.

Para obtener información sobre cómo crear MBeans para administrar los servicios mediante la consola JMX, consulte [Integración de servicios con la consola JMX](/help/sites-developing/jmx-integration.md).

## Mantenimiento de flujo de trabajo {#workflow-maintenance}

Operaciones para administrar instancias de flujo de trabajo en ejecución, completadas, obsoletas y fallidas.

* Dominio: com.adobe.granite.workflow
* Tipo: Mantenimiento

>[!NOTE]
>
>Consulte la [consola de flujo de trabajo](/help/sites-administering/workflows-administering.md) para obtener herramientas de administración de flujo de trabajo adicionales y descripciones de posibles estados de instancias de flujo de trabajo.

### Operaciones {#operations}

**listRunningWorkflowsPerModel** Enumera el número de instancias de flujo de trabajo que se están ejecutando para cada modelo de flujo de trabajo.

* Argumentos: ninguno
* Valor devuelto: datos tabulares que contienen las columnas Count y ModelId.

**listCompletedWorkflowsPerModel** Enumera el número de instancias de flujo de trabajo completadas para cada modelo de flujo de trabajo.

* Argumentos: ninguno
* Valor devuelto: datos tabulares que contienen las columnas Count y ModelId.

**returnWorkflowQueueInfo** muestra información sobre los elementos de flujo de trabajo que se han procesado y que se han puesto en la cola para su procesamiento.

* Argumentos: ninguno
* Valor devuelto: Datos de tabla que contienen las siguientes columnas:

   * Trabajos
   * Nombre de cola
   * Activar tareas
   * Tiempo medio de procesamiento
   * Tiempo medio de espera
   * Trabajos cancelados:
   * Trabajos con errores:
   * Trabajos finalizados
   * Trabajos procesados
   * Trabajos en cola

**returnWorkflowJobTopicInfo** Enumera la información de procesamiento de los trabajos de flujo de trabajo, organizados por tema.

* Argumentos: ninguno
* Valor devuelto: datos tabulares que contienen las siguientes columnas:

   * Nombre del tema
   * Tiempo medio de procesamiento
   * Tiempo medio de espera
   * Trabajos cancelados:
   * Trabajos con errores:
   * Trabajos finalizados
   * Trabajos procesados

**returnFailedWorkflowCount** Muestra el número de instancias de flujo de trabajo con errores. Puede especificar un modelo de flujo de trabajo para consultar o recuperar información de todos los modelos de flujo de trabajo.

* Argumentos:

   * model: ID del modelo que se va a consultar. Para ver un recuento de instancias de flujo de trabajo con errores para todos los modelos de flujo de trabajo, especifique sin valor. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: número de instancias de flujo de trabajo con errores.

**returnFailedWorkflowCountPerModel** Muestra el número de instancias de flujo de trabajo con errores para cada modelo de flujo de trabajo.

* Argumentos: ninguno.
* Valor devuelto: datos tabulares que contienen las columnas Recuento e ID de modelo.

**terminateFailedInstances** Finalice las instancias de flujo de trabajo que hayan fallado. Puede finalizar todas las instancias fallidas o solo las instancias fallidas para un modelo específico. De forma opcional, puede reiniciar las instancias una vez finalizadas. También puede probar la operación para ver los resultados sin realizar realmente la operación.

* Argumentos:

   * Reinicie la instancia: (Opcional) Especifique un valor de `true` para reiniciar las instancias una vez que hayan finalizado. El valor predeterminado de `false` no provoca el reinicio de las instancias de flujo de trabajo terminadas.
   * Ejecución en seco: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar realmente la operación. El valor predeterminado de `false` hace que se realice la operación.
   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias fallidas de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Datos de tabla sobre las instancias que han finalizado, que contienen las columnas siguientes:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**retryFailedWorkItems** intenta ejecutar pasos de elementos de trabajo que han fallado. Puede reintentar todos los elementos de trabajo con errores o solo los elementos de trabajo con errores para un modelo de flujo de trabajo específico. Si lo desea, puede probar la operación para ver los resultados sin realizar realmente la operación.

* Argumentos:

   * Ejecución en seco: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar realmente la operación. El valor predeterminado de `false` hace que se realice la operación.
   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a los elementos de trabajo con errores de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: datos de tabla sobre los elementos de trabajo con errores que se vuelven a intentar, incluidas las columnas siguientes:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**PurgeActive** elimina las instancias de flujo de trabajo activas de una página específica. Se pueden depurar instancias activas para todos los modelos o sólo las instancias de un modelo específico. Si lo desea, puede probar la operación para ver los resultados sin realizar realmente la operación.

* Argumentos:

   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de días desde que se inició el flujo de trabajo: antigüedad de las instancias de flujo de trabajo que se van a depurar, en días.
   * Ejecución en seco: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar realmente la operación. El valor predeterminado de `false` hace que se realice la operación.

* Valor devuelto: datos tabulares sobre las instancias de flujo de trabajo activas que se depuran, incluidas las siguientes columnas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** Devuelve el número de instancias de flujo de trabajo que están obsoletas. Puede recuperar el número de instancias antiguas para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: número de instancias de flujo de trabajo antiguas.

**restartStaleWorkflows**: reinicia las instancias de flujo de trabajo obsoletas. Puede reiniciar todas las instancias antiguas o solo las instancias antiguas de un modelo específico. También puede probar la operación para ver los resultados sin realizar realmente la operación.

* Argumentos:

   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias antiguas de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Ejecución en seco: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar realmente la operación. El valor predeterminado de `false` hace que se realice la operación.

* Valor devuelto: lista de instancias de flujo de trabajo que se reinician.

**fetchModelList** enumera todos los modelos de flujo de trabajo.

* Argumentos: ninguno
* Valor devuelto: datos de tabla que identifican los modelos de flujo de trabajo, incluidas las columnas ModelId y ModelName.

**countRunningWorkflows** Devuelve el número de instancias de flujo de trabajo que se están ejecutando. Puede recuperar el número de instancias en ejecución para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) ID del modelo para el que se devuelve el número de instancias en ejecución. No especificar ningún modelo para devolver el número de instancias en ejecución de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: número de instancias de flujo de trabajo en ejecución.

**countCompletedWorkflows** Devuelve el número de instancias de flujo de trabajo que se han completado. Puede recuperar el número de instancias completadas para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) ID del modelo para el que se devuelve el número de instancias completadas. No especificar ningún modelo para devolver el número de instancias completadas de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: número de instancias de flujo de trabajo completadas.

**purgeCompleted** quita del repositorio los registros de los flujos de trabajo completados de una página específica. Utilice esta operación periódicamente para minimizar el tamaño del repositorio cuando haga un uso intensivo de los flujos de trabajo. Puede depurar instancias completadas para todos los modelos o solo las instancias de un modelo específico. Si lo desea, puede probar la operación para ver los resultados sin realizar realmente la operación.

* Argumentos:

   * Modelo: (Opcional) ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de días transcurridos desde que se completó el flujo de trabajo: número de días durante los cuales las instancias del flujo de trabajo quedaron en el estado completado.
   * Ejecución en seco: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar realmente la operación. El valor predeterminado de `false` hace que se realice la operación.

* Valor devuelto: datos tabulares sobre las instancias de flujo de trabajo completadas que se depuran, incluidas las columnas siguientes:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

## Repositorio {#repository}

Información sobre el repositorio de CRX

* Dominio: com.adobe.granite
* Tipo: repositorio

### Atributos {#attributes}

**Nombre**: el nombre de la implementación del repositorio JCR. Sólo lectura.

**Versión**: La versión de implementación del repositorio. Sólo lectura.

**HomeDir**: directorio donde se encuentra el repositorio. La ubicación predeterminada es &lt;QuickStart_Jar_Location>/crx-quickstart/repository. Sólo lectura.

**NombreCliente**: nombre del cliente al que se emite la licencia de software. Sólo lectura.

**ClaveDeLicencia** La clave de licencia única para esta instalación del repositorio. Sólo lectura.

**AvailableDiskSpace** El espacio en disco disponible para esta instancia del repositorio, en Mbytes. Sólo lectura.

**MaximumNumberOfOpenFiles** El número de archivos que se pueden abrir al mismo tiempo. Sólo lectura.

**SessionTracker** El valor de la variable del sistema crx.debug.session. true indica una sesión de depuración. false indica una sesión normal. Lectura y escritura.

**Descriptores** Un conjunto de pares de clave-valor que representan las propiedades del repositorio. Todas las propiedades son de solo lectura.

<table>
 <tbody>
  <tr>
   <th>Clave</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indica si un nodo y una propiedad del nodo pueden tener el mismo nombre. true indica que se admiten los mismos nombres, false indica que no se admiten. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indica la estabilidad de los identificadores de nodo no referenciables. Los siguientes valores son posibles:
    <ul>
     <li>identifier.stable.indefinite.duration: Los identificadores no cambian.</li>
     <li>identifier.Stability.method.duration: los identificadores pueden cambiar entre llamadas de método.</li>
     <li>identifier.stable.save.duration: Los identificadores no cambian dentro de un ciclo de guardado/actualización.</li>
     <li>identifier.Stability.session.duration: Los identificadores no cambian durante una sesión.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica si se admite el lenguaje de consulta JCR 1.0 XPath. true indica compatibilidad y false indica que no la admite.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>El identificador del sistema tal como se encuentra en el archivo system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica si se admite el lenguaje de consulta JCR 1.0 XPath. true indica compatibilidad y false indica que no la admite.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>La versión de la implementación del repositorio.</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>Indica si se puede cambiar el tipo de nodo principal de un nodo. true indica que puede cambiar el tipo de nodo principal y false indica que no se admite el cambio.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indica si se admite la administración del tipo de nodo. true indica que se admite y false indica que no se admite.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica si se puede anular la propiedad heredada o la definición de nodo secundario de un tipo de nodo. true indica que se admiten invalidaciones y false indica que no se admiten invalidaciones.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true indica que se admite la observación asincrónica de los cambios del repositorio. La compatibilidad con la observación asincrónica permite a las aplicaciones recibir y responder a las notificaciones sobre cada cambio a medida que se produce.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica que la pseudopropiedad jcr:score está disponible en consultas XPath y SQL que incluyen una función jcrfn:contains (en XPath) o CONTAINS (en SQL) para realizar una búsqueda de texto completo.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica que el repositorio admite versiones simples. Con el control de versiones sencillo, el repositorio mantiene una serie secuencial de versiones de un nodo.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica que el repositorio admite la creación y eliminación de espacios de trabajo mediante API.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica que el repositorio admite la adición y eliminación de tipos de nodos de mezcla de un nodo existente.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true indica que el repositorio permite que las definiciones de nodo contengan un elemento principal como elemento secundario. Se puede acceder a un elemento principal mediante la API sin conocer el nombre del elemento.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true indica que tanto LEVEL_1_SUPPORTED como OPTION_XML_IMPORT_SUPPORTED son true.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica que el repositorio proporciona acceso de escritura mediante la API. false indica acceso de solo lectura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica que puede cambiar las definiciones de nodo que están en uso por los nodos existentes.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>La versión de la especificación JCR que implementa el repositorio.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true indica que las aplicaciones pueden realizar una observación en diario del repositorio. con la observación en diario, se puede obtener un conjunto de notificaciones de cambio para un período de tiempo específico. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>Los idiomas de consulta compatibles con el repositorio. Ningún valor indica que no se admitan consultas.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true indica que el repositorio admite la exportación de nodos como código XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true indica que el repositorio admite el registro de tipos de nodo que tienen varias propiedades binarias. false indica que se admite una sola propiedad binaria para un tipo de nodo.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true indica que el repositorio admite el control de acceso para establecer y determinar privilegios de usuario para el acceso a nodos.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true indica que el repositorio admite configuraciones y líneas de base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true indica que el repositorio admite la creación de nodos que se pueden compartir.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>El identificador del clúster de repositorios.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true indica que el repositorio admite consultas almacenadas.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica que el repositorio admite la búsqueda de texto completo.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica el nivel de compatibilidad del repositorio para la herencia de tipo de nodo. Los siguientes valores son posibles:</p> <p>node.type.management.inheritance.minimal: El registro de tipos de nodo principales se limita a los que solo tienen nt:base como supertipo. El registro de los tipos de nodos de mezcla está limitado a los que no tienen supertipo.</p> <p>node.type.management.inheritance.single: El registro de tipos de nodos principales se limita a los que tienen un supertipo. El registro de los tipos de nodos de mezcla está limitado a aquellos con un supertipo como máximo.</p> <p><br /> node.type.management.inheritance.multiple: Los tipos de nodo principales se pueden registrar con uno o varios supertipos. Los tipos de nodos mixin se pueden registrar con cero o más supertipos.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true indica que este nodo de clúster es el nodo maestro preferido del clúster.</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true indica que el repositorio admite transacciones.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>La URL del proveedor del repositorio.</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true indica que el repositorio admite restricciones de valor para las propiedades de nodo.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>una matriz de constantes javax.jcr.PropertyType que representan los tipos de propiedad que puede especificar un tipo de nodo registrado. Una matriz de longitud cero indica que los tipos de nodo registrados no pueden especificar definiciones de propiedades. Los tipos de propiedad son STRING, URI, BOOLEAN, LONG, DOUBLE, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE y UNDEFINED (si se admite)</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica que el repositorio admite la conservación del orden de los nodos secundarios.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>El nombre del proveedor del repositorio.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>Nivel de compatibilidad con uniones en consultas. Los siguientes valores son posibles:</p>
    <ul>
     <li>query.joins.none: no se admiten combinaciones. Las consultas pueden utilizar un selector.</li>
     <li>query.joins.inner: Compatibilidad con uniones internas.</li>
     <li>query.joins.inner.outer: compatibilidad con uniones internas y externas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true indica que el repositorio admite el lenguaje de consulta XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true indica que el repositorio admite la importación de código XML como contenido.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica que el repositorio admite nodos hermanos (nodos con el mismo nodo principal) con los mismos nombres.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true indica que el repositorio admite propiedades de nombre con definiciones residuales. Cuando se admite, el atributo name de una definición de elemento puede ser un asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true indica que el repositorio admite la creación automática de elementos secundarios (nodos o propiedades) de un nodo cuando se crea el nodo.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica que este nodo de repositorio es el nodo maestro del clúster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica que option.xml.export.support es true y query.language tiene una longitud distinta de cero.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true indica que el repositorio admite contenido sin archivar. Los nodos sin archivar no forman parte de la jerarquía del repositorio.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>El nombre de la especificación JCR que implementa el repositorio.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica que el repositorio admite versiones completas.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>El nombre del repositorio.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true indica que el repositorio admite el bloqueo de nodos. El bloqueo permite al usuario impedir temporalmente que otros usuarios realicen cambios.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true indica que el repositorio admite actividades. Las actividades son un conjunto de cambios que se realizan en un espacio de trabajo y que se combinan en otro espacio de trabajo.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica que el repositorio admite propiedades de nodo que pueden tener cero o más valores.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica que el repositorio admite el uso de aplicaciones de administración de retención externas para aplicar directivas de retención al contenido y admite la retención y la liberación.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica que el repositorio admite la administración del ciclo vital.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** nombres de los espacios de trabajo del repositorio. Sólo lectura.

**DataStoreGarbageCollectionDelay** Cantidad de tiempo en milisegundos que la recolección de elementos no utilizados permanece en suspensión después de analizar cada décimo nodo. Lectura y escritura.

**RetrasoDeCopiaDeSeguridad** Cantidad de tiempo en milisegundos que el proceso de copia de seguridad permanece inactivo entre cada paso de la copia de seguridad. Lectura y escritura.

**BackupInProgress** Un valor true indica que se está ejecutando un proceso de copia de seguridad. Sólo lectura.

**BackupProgress** Para la copia de seguridad actual, el porcentaje de todos los archivos de los que se ha realizado una copia de seguridad. Sólo lectura.

**CurrentBackupTarget** Para la copia de seguridad actual, el archivo ZIP donde se almacenan los archivos de copia de seguridad. Cuando una copia de seguridad no está en curso, no aparece ningún valor. Sólo lectura.

**Copia de seguridad correcta** El valor true indica que no se produjeron errores durante la copia de seguridad actual o que no hay ninguna copia de seguridad en curso. false indica que se produjo un error durante la copia de seguridad actual. Sólo lectura.

**ResultadoDeCopiaDeSeguridad** El estado de la copia de seguridad actual. Los siguientes valores son posibles:

* Copia de seguridad en curso: se está ejecutando una copia de seguridad.
* Copia de seguridad cancelada: se ha cancelado la copia de seguridad.
* Copia de seguridad finalizada con error: error durante la copia de seguridad. El mensaje de error proporciona información sobre la causa.
* Copia de seguridad completada: la copia de seguridad se realizó correctamente.
* No se ha ejecutado ninguna copia de seguridad hasta el momento: no hay ninguna copia de seguridad en curso.

Sólo lectura.

**TarOptimizationRunningSince** Hora a la que comenzó el proceso actual de optimización de archivos TAR. Sólo lectura.

**TarOptimizationDelay**: Cantidad de tiempo en milisegundos que el proceso de optimización de TAR permanece inactivo entre cada paso del proceso. Lectura y escritura.

**ClusterProperties** conjunto de pares de clave-valor que representan propiedades y valores de clúster. Cada fila de la tabla representa una propiedad de clúster. Sólo lectura.

**ClusterNodes** Los miembros del clúster del repositorio.

**ClusterId** El identificador de este clúster de repositorio. Sólo lectura.

**ClusterMasterId** Identificador del nodo maestro de este clúster de repositorio. Sólo lectura.

**ClusterNodeId** El identificador de este nodo del clúster de repositorios. Sólo lectura.

### Operaciones {#operations-1}

**createWorkspace** crea un área de trabajo en este repositorio.

* Argumentos:

   * name: Valor de tipo String que representa el nombre del nuevo espacio de trabajo.

* Valor devuelto: ninguno

**runDataStoreGarbageCollection** ejecuta la recolección de elementos no utilizados en los nodos del repositorio.

* Argumentos:

   * delete: valor booleano que indica si se eliminarán los elementos de repositorio no utilizados. El valor true provoca la eliminación de nodos y propiedades no utilizados. El valor false hace que se analicen todos los nodos, pero no se elimina ninguno.

* Valor devuelto: ninguno

**stopDataStoreGarbageCollection** detiene una recolección de elementos no utilizados del almacén de datos en ejecución.

* Argumentos: ninguno
* Valor devuelto: representación de cadena del estado actual

**startBackup** realiza una copia de seguridad de los datos del repositorio en un archivo ZIP.

* Argumentos:

   * `target`: (Opcional) Un valor `String` que representa el nombre del archivo ZIP o directorio en el que archivar los datos del repositorio. Para utilizar un archivo ZIP, incluya la extensión del nombre del archivo ZIP. Para utilizar un directorio, no incluya ninguna extensión de nombre de archivo.

     Para realizar una copia de seguridad incremental, especifique el directorio que se utilizó anteriormente para la copia de seguridad.

     Puede especificar una ruta absoluta o relativa. Las rutas relativas son relativas al elemento principal del directorio crx-quickstart.

     Cuando no especifica ningún valor, se utiliza el valor predeterminado de `backup-currentdate.zip`, donde `currentdate` tiene el formato `yyyyMMdd-HHmm`.

* Valor devuelto: ninguno

**cancelBackup** Detiene el proceso de copia de seguridad actual y elimina el archivo temporal que el proceso creó para archivar datos.

* Argumentos: ninguno
* Valor devuelto: ninguno

**blockRepositoryWrites** bloquea los cambios en los datos del repositorio. El bloque se notifica a todos los agentes de escucha de copia de seguridad del repositorio.

* Argumentos: ninguno
* Valor devuelto: ninguno

**unblockRepositoryWrites** quita el bloque del repositorio. La eliminación del bloque se notifica a todos los agentes de escucha de copia de seguridad del repositorio.

* Argumentos: ninguno
* Valor devuelto: ninguno

**startTarOptimization** Inicia el proceso de optimización del archivo TAR usando el valor predeterminado de tarOptimizationDelay.

* Argumentos: ninguno
* Valor devuelto: ninguno

**stopTarOptimization** detiene la optimización de archivos TAR.

* Argumentos: ninguno
* Valor devuelto: ninguno

**tarIndexMerge** combina los archivos de índice principales de todos los conjuntos TAR. Los archivos de índice principales son archivos con diferentes versiones principales. Por ejemplo, los siguientes archivos se combinan en el archivo index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. Los archivos que se han combinado se eliminan (en el ejemplo anterior, se eliminan index_1_1.tar, index_2_0.tar e index_3_0.tar).

* Argumentos:

   * `background`: valor booleano que indica si se debe ejecutar la operación en segundo plano para que la consola web se pueda utilizar durante la ejecución. El valor true ejecuta la operación en segundo plano.

* Valor devuelto: ninguno

**convertClusterMaster**: establece este nodo de repositorio como el nodo maestro del clúster. Si no es así, este comando detiene el agente de escucha de la instancia maestra actual e inicia un agente de escucha maestro en el nodo actual. A continuación, este nodo se establece como nodo maestro y se reinicia, lo que provoca que todos los demás nodos del clúster (es decir, aquellos que están controlados por el nodo maestro) se conecten a esta instancia.

* Argumentos: ninguno
* Valor devuelto: ninguno

**joinCluster** Agrega este repositorio a un clúster como un nodo controlado por el maestro de clúster. Proporcione un nombre de usuario y una contraseña para fines de autenticación. La conexión utiliza autenticación básica. Las credenciales de seguridad se codifican en base 64 antes de enviarse al servidor.

* Argumentos:

   * `master`: valor de cadena que representa la dirección IP o el nombre de equipo del equipo que ejecuta el nodo del repositorio principal.
   * `username`: nombre que se usará para autenticarse en el clúster.
   * `password`: contraseña que se va a usar para la autenticación.

* Valor devuelto: ninguno

**travversalCheck** atraviesa y opcionalmente corrige incoherencias en un subárbol que comienza en un nodo específico. Esto se trata en detalle en la documentación sobre Administradores de persistencia.

**consistencyCheck and opcionalmente corrige la coherencia en el almacén de datos.** Esto se trata en detalle en la documentación del almacén de datos.

## Estadísticas del repositorio (TimeSeries) {#repository-statistics-timeseries}

El valor del campo SerieTemporal para cada tipo de estadística que define `org.apache.jackrabbit.api.stats.RepositoryStatistics`.

* Dominio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Nombre: uno de los siguientes valores de la clase `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * PAQUETE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * PAQUETE_CONTADOR
   * PAQUETE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * PAQUETE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * PAQUETE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### Atributos {#attributes-1}

Se proporcionan los atributos siguientes para cada tipo de estadística del que se informa:

* ValuePerSecond: valor medido por segundo en el último minuto. Sólo lectura.
* ValuePerMinute: valor medido por minuto durante la última hora. Sólo lectura.
* ValuePerHour: Valor medido por hora durante la última semana. Sólo lectura.
* ValuePerWeek: valor medido por semana durante los últimos tres años. Sólo lectura.

## Estadísticas de consulta del repositorio {#repository-query-stats}

Información estadística sobre consultas del repositorio.

* Dominio: com.adobe.granite
* Tipo: QueryStat

### Atributos {#attributes-2}

**ConsultasLentas** Información acerca de las consultas del repositorio que han tardado más tiempo en completarse. Sólo lectura.

**SlowQueriesQueueSize** Número máximo de consultas que se incluirán en la lista SlowQueries. Lectura-escritura.

**ConsultasPopulares** Información sobre las consultas de repositorio que se han producido con mayor frecuencia. Sólo lectura.

**PopularQueriesQueueSize** Número máximo de consultas en la lista PopularQueries. Lectura-escritura.

### Operaciones {#operations-2}

**clearSlowQueriesQueue** quita todas las consultas de la lista SlowQueries.

* Argumentos: ninguno
* Valor devuelto: ninguno

**clearPopularQueriesQueue** quita todas las consultas de la lista PopularQueries.

* Argumentos: ninguno
* Valor devuelto: ninguno

## Agentes de replicación {#replication-agents}

Supervise los servicios de cada agente de replicación. Al crear un agente de replicación, el servicio aparece automáticamente en la consola JMX.

* **Dominio:** com.adobe.granite.replication
* **Tipo:** agente
* **Nombre:** sin valor
* **Propiedades:** {id=&quot;*Nombre*&quot;}, donde *Nombre* es el valor de la propiedad Nombre del agente.

### Atributos {#attributes-3}

**Id** Valor de cadena que representa el identificador de la configuración del agente de replicación. Varios agentes pueden utilizar la misma configuración. Sólo lectura.

**Válido** Un valor booleano que indica si el agente está configurado correctamente:

* `true`: configuración válida.
* `false` : la configuración contiene errores.

Sólo lectura.

**Habilitado** Un valor booleano que indica si el agente está habilitado:

* `true`: Habilitado.
* `false`: deshabilitado.

**QueueBlocked** Valor booleano que indica si la cola existe y está bloqueada:

* `true`: Bloqueado. Está pendiente un reintento automático.
* `false`: no está bloqueado o no existe.

Sólo lectura.

**QueuePaused** Un valor booleano que indica si la cola de trabajos está en pausa:

* `true`: en pausa (suspendido)
* `false`: no está en pausa o no existe.

Lectura-escritura.

**QueueNumEntries** Valor int que representa el número de trabajos en la cola del agente. Sólo lectura.

**QueueStatusTime** Valor de fecha que indica la hora en el servidor en que se obtuvieron los valores de estado mostrados. El valor corresponde a la hora en que se cargó la página. Sólo lectura.

**QueueNextRetryTime** Para colas bloqueadas, un valor Date que indica cuándo se produce el siguiente reintento automático. Cuando no aparece ningún tiempo, la cola no se bloquea. Sólo lectura.

**QueueProcessingSince** Valor de fecha que indica cuándo comenzó el procesamiento del trabajo actual. Cuando no aparece ningún tiempo, la cola está bloqueada o inactiva. Sólo lectura.

**QueueLastProcessTime** Valor de fecha que indica cuándo se completó el trabajo anterior. Sólo lectura.

### Operaciones {#operations-3}

**queueForceRetry** Para colas bloqueadas, envía el comando retry a la cola.

* Argumentos: ninguno
* Valor devuelto: ninguno

**queueClear** Quita todos los trabajos de la cola.

* Argumentos: ninguno
* Valor devuelto: ninguno

## Motor de Sling {#sling-engine}

Proporciona estadísticas sobre las solicitudes HTTP para que pueda supervisar el rendimiento del servicio SlingRequestProcessor.

* Dominio: org.apache.sling
* Tipo: motor
* Propiedades: {service=RequestProcessor}

### Atributos {#attributes-4}

**RequestsCount**: el número de solicitudes que se han producido desde que se restablecieron las estadísticas por última vez.

**MinRequestDurationMsec** La cantidad de tiempo más corta (en milisegundos) necesaria para procesar una solicitud desde que se restablecieron las estadísticas por última vez.

**MaxRequestDurationMsec** La cantidad de tiempo más larga (en milisegundos) necesaria para procesar una solicitud desde que se restablecieron las estadísticas por última vez.

**StandardDeviationDurationMsec** Desviación estándar del tiempo necesario para procesar solicitudes. La desviación estándar se calcula utilizando todas las solicitudes desde el último restablecimiento de las estadísticas.

**MeanRequestDurationMsec** Cantidad media de tiempo necesaria para procesar una solicitud. La media se calcula utilizando todas las solicitudes desde el último restablecimiento de las estadísticas

### Operaciones {#operations-4}

**resetStatistics** establece todas las estadísticas en cero. Restablezca las estadísticas cuando necesite analizar el rendimiento del procesamiento de la solicitud durante un lapso de tiempo específico.

* Argumentos: ninguno
* Valor devuelto: ninguno

**id**: la representación de cadena del ID del paquete.

**instalado** Un valor booleano que indica si el paquete está instalado:

* `true`: instalado.
* `false`: no instalado.

**installerBy**: ID del usuario que instaló el paquete por última vez.

**installerDate**: la fecha en la que se instaló el paquete por última vez.

**size** Un valor largo que contiene el tamaño del paquete en bytes.


## Lanzador rápido {#quickstart-launcher}

Información sobre el proceso de inicio y el lanzador de inicio rápido.

* Dominio: com.adobe.granite.quickstart
* Tipo: lanzador

### Operaciones {#operations-5}

**registro**

Muestra un mensaje en la ventana Inicio rápido.

Argumentos:

* p1: Un valor `String` que representa el mensaje que se va a mostrar.
* Valor devuelto: ninguno

**startupFinished**

Llama al método startupFinished del iniciador del servidor. El método intenta abrir la página de bienvenida en un explorador web.

* Argumentos: ninguno
* Valor devuelto: ninguno

**startupProgress**

Establece el valor de finalización del proceso de inicio del servidor. La barra de progreso de la ventana QuickStart representa el valor de finalización.

* Argumentos:
   * p1: Valor flotante que representa la parte completa del proceso de inicio, como fracción. El valor debe estar entre cero y uno. Por ejemplo, 0,3 indica que se ha completado el 30 %.
* Valor devuelto: ninguno.

## Servicios de terceros {#third-party-services}

Varios recursos de servidor de terceros instalan MBeans que exponen atributos y operaciones a la consola JMX. En la siguiente tabla se enumeran los recursos de terceros y se proporcionan vínculos a más información.

<table>
 <tbody>
  <tr>
   <th>Dominio</th>
   <th>Tipo</th>
   <th>Clase de MBean</th>
  </tr>
  <tr>
   <td>Implementación JMI</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilación</li>
     <li>GarbageCollector</li>
     <li>Memoria</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>OperatingSystem</li>
     <li>Tiempo de ejecución</li>
     <li>Subprocesamiento</li>
    </ul> </td>
   <td>paquete <a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a></td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>marco</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td>Paquete <a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a></td>
  </tr>
 </tbody>
</table>

## Uso de la consola JMX {#using-the-jmx-console}

La consola JMX muestra información sobre varios servicios que se ejecutan en el servidor:

* Atributos: propiedades del servicio como configuraciones o datos en tiempo de ejecución. Los atributos pueden ser de solo lectura o de lectura-escritura.
* Operaciones: comandos que se pueden invocar en el servicio.

Los MBean que se implementan con un servicio OSGi exponen atributos y operaciones de servicio a la consola. El MBean determina los atributos y las operaciones que se exponen, y si los atributos son de sólo lectura o de lectura-escritura.

La página principal de la consola JMX incluye una tabla de servicios. Cada fila de la tabla representa un servicio que se expone mediante un MBean.

1. Abra la consola web y haga clic en la pestaña JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Haga clic en un valor de celda de un servicio para ver sus atributos y operaciones.
3. Para cambiar un valor de atributo, haga clic en el valor, especifique el valor en el cuadro de diálogo que aparece y haga clic en Guardar.
4. Para invocar una operación de servicio, haga clic en el nombre de la operación, especifique valores de argumento en el cuadro de diálogo que aparece y haga clic en Invocar.

## Uso de aplicaciones JMX externas para la monitorización {#using-external-jmx-applications-for-monitoring}

CRX permite que las aplicaciones externas interactúen con Managed Beans (MBeans) a través de [Java Management Extensions (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). El uso de consolas genéricas como [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) o aplicaciones de supervisión específicas del dominio permite obtener y establecer configuraciones y propiedades de CRX, así como supervisar el rendimiento y el uso de recursos.

### Uso de JConsole para conectarse a CRX {#using-jconsole-to-connect-to-crx}

Para conectarse a CRX mediante JConsole, siga estos pasos:

1. Abra una ventana de terminal.
1. Introduzca el siguiente comando:

   `jconsole`

JConsole se iniciará y aparecerá la ventana de JConsole.

### Conexión a un proceso local de CRX {#connecting-to-a-local-crx-process}

JConsole mostrará una lista de los procesos locales de la máquina virtual Java. La lista contendrá dos procesos de inicio rápido. Seleccione el proceso &quot;CHILD&quot; de inicio rápido de la lista de procesos locales (normalmente el que tiene el PID más alto).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Conexión a un proceso remoto de CRX {#connecting-to-a-remote-crx-process}

Para conectarse a un proceso remoto de CRX, la JVM que aloja el proceso remoto de CRX debe estar habilitada para aceptar conexiones remotas de JMX.

Para habilitar conexiones JMX remotas, se debe establecer la siguiente propiedad del sistema al iniciar la JVM:

`com.sun.management.jmxremote.port=portNum`

En la propiedad anterior, `portNum` es el número de puerto a través del cual desea habilitar conexiones RMI JMX. Asegúrese de especificar un número de puerto no utilizado. Además de publicar un conector RMI para acceso local, al establecer esta propiedad se publica un conector RMI adicional en un registro privado de sólo lectura en el puerto especificado con un nombre conocido, &quot;jmxrmi&quot;.

De forma predeterminada, al habilitar el agente JMX para la monitorización remota, utiliza la autenticación de contraseña basada en un archivo de contraseña que debe especificarse mediante la siguiente propiedad del sistema al iniciar la VM de Java:

`com.sun.management.jmxremote.password.file=pwFilePath`

Consulte la [documentación JMX relevante](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) para obtener instrucciones detalladas sobre cómo configurar un archivo de contraseña.

Ejemplo:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Uso de los MBeans proporcionados por CRX {#using-the-mbeans-provided-by-crx}

Después de conectarse al proceso de inicio rápido, JConsole proporciona una serie de herramientas de monitorización generales para la JVM en la que CRX se está ejecutando.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Para acceder a las opciones de monitorización y configuración internas de CRX, vaya a la pestaña MBeans y, en el árbol de contenido jerárquico de la izquierda, seleccione la sección Attributes or Operations que le interese. Por ejemplo, la sección com.adobe.granite/Repository/Operations.

En esa sección, seleccione el atributo u operación que desee en el panel izquierdo.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
