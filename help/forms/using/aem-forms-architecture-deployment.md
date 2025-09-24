---
title: Arquitectura y topologías de implementación para AEM Forms
description: Detalles de arquitectura para AEM Forms y topologías recomendadas para clientes nuevos y existentes de AEM que actualicen de LiveCycle ES4 a AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 23ffbaa6-1bd9-48c3-afa3-19737bb15de0
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 90%

---

# Arquitectura y topologías de implementación para AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html?lang=es).

## Arquitectura {#architecture}

AEM Forms es una aplicación implementada en AEM como paquete de AEM. El paquete se conoce como paquete de complementos de AEM Forms. El paquete de complementos de AEM Forms contiene ambos servicios (proveedores de API), que se implementan en el contenedor OSGi de AEM y servlets o JSP (que proporcionan la funcionalidad de API de front-end y REST) administrados por el marco de trabajo de AEM Sling. El siguiente diagrama muestra esta configuración:

![arquitectura](assets/architecture.png)

La arquitectura para AEM Forms incluye los siguientes componentes:

* **Servicios principales de AEM:** servicios básicos que proporciona AEM a una aplicación implementada. Estos servicios incluyen un repositorio de contenido compatible con JCR, un contenedor de servicio OSGI, un motor de flujo de trabajo, un repositorio de confianza, un repositorio de claves, etc. Estos servicios están disponibles para la aplicación de AEM Forms, pero los paquetes de AEM Forms no los proporcionan. Estos servicios forman parte integral de la pila de AEM general y varios componentes de AEM Forms utilizan estos servicios.
* **Servicios de Forms:** proporcionan funciones relacionadas con los formularios, como crear, combinar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos y descodificar formularios de barras codificados. Estos servicios están disponibles públicamente para el consumo mediante el código personalizado que se ha implementado en AEM.
* **Capa web:** JSP o servlets, creados sobre servicios comunes y de formularios, que proporcionan las siguientes funcionalidades:

   * **Crear front-end**: una interfaz de usuario de creación y administración de formularios para crear y administrar formularios.
   * **Front-end Procesar y enviar formularios**: interfaz de usuario final para que la utilicen los usuarios finales de AEM Forms (por ejemplo, los ciudadanos que acceden a un sitio web del Gobierno). Proporciona funciones de representación de formularios (formulario de visualización en un explorador web) y envío.
   * **API de REST**: los JSP y los servlets exportan un subconjunto de servicios de formularios para el que lo consuman de manera remota clientes basados en HTTP, como el SDK móvil de formularios.

**AEM Forms en OSGi:** AEM Forms en un entorno OSGi es AEM Author estándar o AEM Publish con el paquete de AEM Forms implementado en él. Puede ejecutar AEM Forms en OSGi en un [entorno de servidor único, configuración de granjas y de clústeres](/help/sites-deploying/recommended-deploys.md). La configuración de clúster solo está disponible para instancias de autor de AEM.

<!--

**AEM Forms on JEE:** AEM Forms on JEE is AEM Forms server running on JEE stack. It has AEM Author with AEM Forms add-on packages and additional AEM Forms JEE capabilities co-deployed on a single JEE stack running on an application server. You can run AEM Forms on JEE in single-server and clustered setups. AEM Forms on JEE is required only to run document security, process management, and for LiveCycle customers upgrading to AEM Forms. Here are a few additional scenarios to use AEM Forms on JEE:

* **HTML workspace support (for customers using HTML workspace):** AEM Forms on JEE enables single sign-on with Processing instances, serves certain assets rendered on Processing instances, and handles submission of forms rendered within the HTML workspace.
* **Advanced additional form/interactive communication data processing**: AEM Forms on JEE can be utilized for additionally processing form/interactive communication data (and saving the results to a suitable data store) in complex use-cases where advanced process-management capabilities are required.

AEM Forms on JEE also includes provides following supporting services to the AEM components:

* **Integrated user management:** Allows users of AEM Forms on JEE to be recognized as AEM forms on OSGi users and helps enable SSO for both OSGi and JEE users. This is required for scenarios where single sign-on between AEM forms on OSGi and AEM Forms on JEE is required (for example, HTML workspace).
* **Asset hosting:** AEM Forms on JEE can serve assets (for example, HTML5 forms) rendered on AEM Forms on OSGi.

-->

La interfaz de usuario de creación de AEM Forms no es compatible con la creación de documentos de registro (DOR), formularios PDF y formularios HTML5. Estos recursos están diseñados con la aplicación independiente Forms Designer y se cargan individualmente en AEM Forms Manager. <!--Alternatively, for AEM Forms on JEE, forms can be designed as application (in AEM Forms Workbench) assets and deployed into AEM Forms on JEE server.-->

AEM Forms en OSGi <!--and AEM Forms on JEE both--> tiene capacidades de flujo de trabajo. Puede generar e implementar rápidamente flujos de trabajo básicos para diversas tareas en los formularios de AEM en OSGi.<!--, without having to install the full-fledged Process Management capability of AEM Forms on JEE. There is some difference in the [features of Form-centric workflow on AEM Forms on OSGi and Process Management capability of AEM Forms on JEE](capabilities-osgi-jee-workflows.md). The development and management of Form-centric workflows on AEM Forms on OSGi uses the familiar AEM Workflow and AEM Inbox capabilities.-->

## Terminologías {#terminologies}

La siguiente imagen muestra varias configuraciones del servidor de AEM Forms y sus componentes que se utilizan en una implementación típica de AEM Forms:

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**Autor:** una instancia de autor es un servidor de AEM Forms que se ejecuta en el modo de ejecución estándar de Autor. <!--It can be AEM Forms on JEE or AEM Forms on OSGi environment.--> está dirigido a usuarios internos, diseñadores de formularios y de comunicaciones interactivas y desarrolladores. Habilita las siguientes funcionalidades:

* **Crear y administrar formularios y comunicaciones interactivas:** los diseñadores y desarrolladores pueden crear y editar formularios adaptables y comunicaciones interactivas, cargar otros tipos de formularios creados externamente, por ejemplo, formularios creados en Adobe Forms Designer y administrar estos recursos mediante la consola de Forms Manager.
* **Publicar formularios y comunicaciones interactivas:** los recursos alojados en una instancia de autor se pueden publicar en una instancia de publicación para realizar operaciones de tiempo de ejecución. La publicación de recursos utiliza las funciones de replicación de AEM. Adobe recomienda que se configure un agente de replicación en todas las instancias de autor para insertar manualmente los formularios publicados en las instancias de procesamiento y que se configure otro agente de replicación en las instancias de procesamiento con el activador *Recepción* habilitado para replicar automáticamente los formularios recibidos en las instancias de publicación.

**Publicación:** una instancia de publicación es un servidor de AEM Forms que se ejecuta en el modo de ejecución de publicación estándar. Las instancias de publicación están destinadas a los usuarios finales de aplicaciones basadas en formularios como, por ejemplo, los usuarios que acceden a un sitio web público y envían formularios. Habilita las siguientes funcionalidades:

* Procesar y enviar formularios para usuarios finales.
* Transportar datos de formulario enviados sin procesar a instancias de procesamiento para su procesamiento y almacenamiento posteriores en el sistema final de registro. La implementación predeterminada que se proporciona en AEM Forms logra esto al utilizar las capacidades de replicación inversa de AEM. También hay una implementación alternativa disponible para insertar directamente los datos del formulario en servidores de procesamiento en lugar de guardarlos localmente primero (siendo este último un requisito previo para que se active la replicación inversa). Los clientes que tengan dudas sobre el almacenamiento de datos confidenciales en instancias de publicación pueden participar en esto [implementación alternativa](/help/forms/using/configuring-draft-submission-storage.md), ya que las instancias de procesamiento normalmente se encuentran en una zona más segura.
* Presentar y enviar comunicaciones y cartas interactivas: se procesa una comunicación interactiva y una carta en las instancias de publicación y los datos correspondientes se envían a instancias de procesamiento para su almacenamiento y posprocesamiento. Los datos se pueden guardar localmente en una instancia de publicación y replicarse de forma inversa en una instancia de procesamiento (opción predeterminada) posteriormente, o insertarse directamente en la instancia de procesamiento sin guardar en la instancia de publicación. Esta última implementación es útil para los clientes conscientes de la seguridad.

**Procesamiento:** instancia de AEM Forms que se ejecuta en el modo de ejecución de Autor sin usuarios asignados al grupo de administrador de formularios. Puede implementar <!--AEM Forms on JEE or--> AEM Forms en OSGi como instancia de procesamiento. Los usuarios no están asignados para garantizar que las actividades de creación y administración de formularios no se realicen en la instancia de procesamiento y solo se produzcan en la instancia de autor. Una instancia de procesamiento habilita las siguientes funcionalidades:

* **Procesar los datos de formulario sin procesar procedentes de una instancia de publicación:** esto se logra principalmente en una instancia de procesamiento a través de flujos de trabajo de AEM que se activan cuando llegan los datos. Los flujos de trabajo pueden utilizar el paso Modelo de datos de formulario que se proporciona de forma predeterminada para archivar los datos o el documento en un almacén de datos adecuado.
* **Almacenamiento seguro de datos de formulario**: el procesamiento proporciona un repositorio detrás del firewall para los datos de formulario sin procesar que están aislados de los usuarios. Ni los diseñadores de formularios de la instancia de autor ni los usuarios finales de la instancia de publicación pueden acceder a este repositorio.

  >[!NOTE]
  >
  >Adobe recomienda utilizar un repositorio de datos de terceros para guardar los datos procesados finales en lugar de utilizar el repositorio de AEM.

* **Almacenar y posprocesar los datos de correspondencia que llegan desde una instancia de publicación:** los flujos de trabajo de AEM realizan el posprocesamiento opcional de las definiciones de cartas correspondientes. Estos flujos de trabajo pueden guardar los datos procesados finales en un repositorio de datos externo adecuado.

* **Alojamiento en el espacio de trabajo HTML**: una instancia de procesamiento aloja el front-end para el espacio de trabajo HTML. El espacio de trabajo HTML proporciona la interfaz de usuario para la asignación de tareas/grupos asociados para los procesos de revisión y aprobación.

Una instancia de procesamiento está configurada para ejecutarse en el modo de ejecución de Autor debido a lo siguiente:

* Permite la replicación inversa de los datos de formulario sin procesar de una instancia de publicación. El controlador de almacenamiento de datos predeterminado requiere la característica de replicación inversa.
* Los flujos de trabajo de AEM, que son el principal medio de procesar los datos de formulario sin procesar que llegan desde una instancia de publicación, se recomiendan para ejecutarse en un sistema de estilo Autor.

<!--

## Sample physical topologies for AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

The AEM Forms on JEE topologies recommended below are mainly for customers upgrading from LiveCycle or a previous version of AEM Forms on JEE. Adobe recommends using AEM Forms on OSGi for fresh installations. A fresh installation of AEM Forms on JEE only recommended for using Document Security and Process Management capabilities.

### Topology for using document services or document security capabilities {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms customers planning to use only document services or document security capabilities can have a topology similar to the one displayed below. This topology recommends using a single instance of AEM Forms. You can also create a cluster or farm of AEM Forms servers, if necessary. This topology is recommended when most users programmatically access capabilities of AEM Forms server and intervention through the user interface is minimum. The topology is helpful in batch processing operations of document services. For example, using output service to create hundreds of non-editable PDF documents on daily basis.

Although, AEM Forms lets you set up and run all the functionalities from a single server, yet, you should do capacity planning, load balancing, and set up dedicated servers for specific capabilities in a production environment. For example, for an environment using the PDF Generator service to convert thousands of pages a day and add digital signatures to limit access to documents, set up separate AEM Forms servers for the PDF Generator service and digital signature capabilities. It helps provide optimum performance and scale the servers independent of each other.

![basic-features](assets/basic-features.png)

### Topology for using AEM Forms process management {#topology-for-using-aem-forms-process-management}

AEM Forms customers planning to use AEM Forms process management features, for example, HTML Workspace can have a topology similar to the one displayed below. The AEM Forms on JEE server can be in a single server or cluster configuration.

If you are upgrading from LiveCycle ES4, this topology closely mirrors with what you already have in LiveCycle except for the addition of AEM Author built-in to AEM Forms on JEE. Moreover, there is no change in the clustering requirements for customers performing an upgrade. If you were using AEM Forms in a clustered environment, you can continue with same in AEM 6.5 Forms. For a fresh installation of AEM Forms of JEE for using HTML Workspace, running AEM author instance built-in to the JEE environment is an additional requirement.

Form data store is a third-party data store used for storing final processed data of forms and interactive communications. This is an optional element in the topology. You can also choose to set up a processing instance and use its repository as the final system-of-record system, if necessary.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

The topology is recommended to the customers planning to use AEM Forms on JEE server for process management capabilities (HTML Workspace) without using any post-processing, adaptive forms, HTML5 forms, and interactive communication capabilities.

### Topology for using adaptive forms, HTML5 forms, interactive communication capabilities {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms customers planning to use AEM Forms data capture capabilities, for example, adaptive forms, HTML5 Forms, PDF Forms, can have a topology similar to the one displayed below. This topology is also recommended for using interactive communication capabilities of AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

You can make the following changes/customizations to the above-suggested topology:

* Using HTML Workspace and AEM Forms app requires an AEM author or processing instance. You can use the AEM author instance built-in to AEM Forms on JEE server instead of setting up an additional external AEM author server.
* An AEM Author or Processing instance is required only for Forms-centric workflows on OSGi, adaptive forms, forms portal, and interactive communication.
* interactive communication Agent UI is generally run within the organization. So, you can keep a publish server for Agent UI within the private network.
* AEM forms on OSGi instance built-in to AEM Forms on JEE server can also run Forms-centric workflows on OSGi and Watched Folders.

-->

## Ejemplo de topologías físicas para usar AEM Forms en OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topología para la captura de datos, comunicaciones interactivas, flujos de trabajo centrados en formularios sobre las capacidades de OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Los clientes de AEM Forms que planean utilizar las funciones de captura de datos de AEM Forms, por ejemplo, los formularios adaptables, formularios HTML5 o formularios PDF, pueden tener una topología similar a la que se muestra a continuación. Esta topología también se recomienda para utilizar comunicaciones interactivas y flujos de trabajo centrados en Forms en la capacidad OSGi, por ejemplo, para utilizar la bandeja de entrada de AEM y la aplicación de AEM Forms para flujos de trabajo de procesos empresariales.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topología para el uso de las funciones de carpeta vigilada para el procesamiento por lotes sin conexión {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Los clientes de AEM Forms que planean utilizar carpetas vigiladas para el procesamiento por lotes pueden tener una topología similar a la que se muestra a continuación. La topología muestra un entorno agrupado, pero decide utilizar una instancia única o una granja de servidores de AEM Forms en función de la carga. La fuente de datos de terceros es su propio sistema de registro. Actúa como fuente de entrada para carpetas vigiladas. La topología también muestra los resultados en forma de archivo impreso. También puede almacenar el contenido de salida en un sistema de archivos, enviarlo por correo electrónico y utilizar otros métodos personalizados para consumir resultados.

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topología para utilizar las funcionalidades de servicios de documentos para el procesamiento sin conexión basado en API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Los clientes de AEM Forms que planean utilizar únicamente la funcionalidad de servicios de documentos pueden tener una topología similar a la que se muestra a continuación. Esta topología recomienda utilizar un clúster de AEM Forms en servidores OSGi. Esta topología se recomienda cuando la mayoría de los usuarios acceden mediante programación (mediante API) al servidor de AEM Forms y la intervención a través de la interfaz de usuario es mínima. La topología es muy útil en varios casos de cliente de software. Por ejemplo, varios clientes que utilizan el servicio Generador de PDF para crear documentos PDF bajo demanda.

Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, en el caso de un entorno que utiliza el servicio PDF Generator para convertir miles de páginas al día y varios formularios adaptables para capturar datos, deberá configurar servidores de AEM Forms independientes para el servicio PDF Generator y las capacidades relacionadas con los formularios adaptables. Esto permite proporcionar un rendimiento óptimo y escalar los servidores de forma independiente entre sí.

![offline-api-based-processing](assets/offline-api-based-processing.png)
