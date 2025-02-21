---
title: Directrices de rendimiento
description: Este artículo proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2937'
ht-degree: 5%

---

# Directrices de rendimiento{#performance-guidelines}

Esta página proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de AEM. Si es nuevo en AEM, revise las siguientes páginas antes de empezar a leer las directrices de rendimiento:

* [Conceptos básicos de AEM](/help/sites-deploying/deploy.md#basic-concepts)
* [Información general sobre el almacenamiento en AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)

A continuación se ilustran las opciones de implementación disponibles para AEM (desplácese para ver todas las opciones):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Producto</strong></p> </td>
   <td><p><strong>Topología</strong></p> </td>
   <td><p><strong>Sistema operativo</strong></p> </td>
   <td><p><strong>Servidor de aplicaciones</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Seguridad</strong></p> </td>
   <td><p><strong>Microkernel</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Indexación</strong></p> </td>
   <td><p><strong>Servidor web</strong></p> </td>
   <td><p><strong>Explorador</strong></p> </td>
   <td><p><strong>Experience Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Sin AH</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>Segmento</p> </td>
   <td><p>Propiedad</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Público destinatario</p> </td>
  </tr>
  <tr>
   <td><p>Recursos</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris™</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM®</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>Archivo</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Análisis</p> </td>
  </tr>
  <tr>
   <td><p>Comunidades</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Red Hat®</p> </td>
   <td><p>WebSphere®</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Formularios</p> </td>
   <td><p>Autor-Descarga</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>Dispositivo móvil</p> </td>
   <td><p>Author-Cluster</p> </td>
   <td><p>IBM® AIX®</p> </td>
   <td><p>JBoss®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Público</p> </td>
  </tr>
  <tr>
   <td><p>En varios sitios</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Recursos</p> </td>
  </tr>
  <tr>
   <td><p>Comercio</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>SO APPLE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Activación</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Dispositivo móvil</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Doc Security</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Administración de procesos</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>aplicación de escritorio</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Las directrices de rendimiento se aplican principalmente a AEM Sites.

## Cuándo utilizar las directrices de rendimiento {#when-to-use-the-performance-guidelines}

Utilice las directrices de rendimiento en las siguientes situaciones:

* **Implementación por primera vez**: Cuando planee implementar AEM Sites o Assets por primera vez, es importante entender las opciones disponibles. Especialmente al configurar el Micro Kernel, el Almacén de nodos y el Almacén de datos (en comparación con la configuración predeterminada). Por ejemplo, cambiar la configuración predeterminada del almacén de datos para TarMK a almacén de datos de archivo.
* **Actualización a una nueva versión**: Al actualizar a una nueva versión, es importante comprender las diferencias de rendimiento en comparación con el entorno en ejecución. Por ejemplo, actualizar de AEM 6.1 a 6.2 o de AEM 6.0 CRX2 a 6.2 OAK.
* **El tiempo de respuesta es lento**: Cuando la arquitectura de Nodestore seleccionada no cumple con sus requisitos, es importante entender las diferencias de rendimiento en comparación con otras opciones de topología. Por ejemplo, implementar TarMK en lugar de MongoMK, o usar un almacén de datos de archivo en lugar de un almacén de datos de Amazon S3 o Microsoft® Azure.
* **Agregar más autores**: Cuando la topología TarMK recomendada no cumple los requisitos de rendimiento y el nodo Autor ha alcanzado la capacidad máxima disponible, comprenda las diferencias de rendimiento. Compare MongoMK con tres o más nodos de Author. Por ejemplo, implementar MongoMK en lugar de TarMK.
* **Agregar más contenido**: Cuando la arquitectura de almacén de datos recomendada no cumple con sus requisitos, es importante entender las diferencias de rendimiento en comparación con otras opciones del almacén de datos. Ejemplo: uso del Almacén de datos de Amazon S3 o Microsoft® Azure en lugar de un Almacén de datos de archivo.

## Introducción {#introduction}

En este capítulo se ofrece una descripción general de la arquitectura de AEM y sus componentes más importantes. También proporciona directrices de desarrollo y describe los escenarios de prueba utilizados en las pruebas de referencia de TarMK y MongoMK.

### La plataforma de AEM {#the-aem-platform}

La plataforma de AEM consta de los siguientes componentes:

![chlimage_1](assets/chlimage_1a.png)

Para obtener más información sobre la plataforma AEM, consulte [Qué es AEM](/help/sites-deploying/deploy.md#what-is-aem).

### La arquitectura de AEM {#the-aem-architecture}

Una implementación de AEM consta de tres componentes básicos importantes. La **instancia de autor** que utilizan los autores, editores y aprobadores de contenido para crear y revisar contenido. Cuando se aprueba el contenido, se publica en un segundo tipo de instancia denominado **Instancia de publicación** desde donde los usuarios finales tienen acceso a él. El tercer bloque de creación es **Dispatcher**, que es un módulo que administra el almacenamiento en caché y el filtrado de URL y que está instalado en el servidor web. Para obtener información adicional acerca de la arquitectura de AEM, vea [Escenarios de implementación típicos](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernels {#micro-kernels}

Los microkernels actúan como administradores de persistencia en AEM. Existen tres tipos de Micro Kernels utilizados con AEM: TarMK, MongoDB y Base de datos relacional (con soporte restringido). Elegir una que se ajuste a sus necesidades depende del propósito de su instancia y del tipo de implementación que esté considerando. Para obtener información adicional sobre Micro Kernels, consulte la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

En AEM, los datos binarios se pueden almacenar de forma independiente de los nodos de contenido. La ubicación donde se almacenan los datos binarios se denomina **Almacén de datos**, mientras que la ubicación de los nodos de contenido y las propiedades se denomina **Almacén de nodos**.

>[!NOTE]
>
>Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes tanto para las instancias de autor de AEM como para las de publicación.

>[!CAUTION]
>
>El micronúcleo de la base de datos relacional tiene compatibilidad restringida. Póngase en contacto con el [Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) antes de usar este tipo de microkernel.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Almacén de datos {#data-store}

Cuando se trata de un gran número de binarios, se recomienda utilizar un almacén de datos externo en lugar de los almacenes de nodos predeterminados para maximizar el rendimiento. Por ejemplo, si el proyecto requiere muchos recursos multimedia, almacenarlos en el almacén de datos de Azure/S3 o de archivos hará que el acceso a ellos sea más rápido que almacenarlos directamente en un MongoDB.

Para obtener más información sobre las opciones de configuración disponibles, consulte [Configuración del nodo y los almacenes de datos](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe recomienda elegir la opción de implementar AEM en Azure o Amazon Web Service (AWS) mediante Adobe Managed Services. Los clientes se benefician de un equipo que tiene la experiencia y las habilidades de implementar y operar AEM en estos entornos de computación en la nube. Ver [documentación adicional sobre Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).
>
>Para obtener recomendaciones sobre cómo implementar AEM en Azure o AWS, fuera de Adobe Managed Services, Adobe recomienda trabajar directamente con el proveedor de la nube. O trabaje con uno de los socios de Adobe que admita la implementación de AEM en el entorno de nube que elija. El proveedor o socio de nube seleccionado es responsable de las especificaciones de tamaño, el diseño y la implementación de la arquitectura que admiten para satisfacer los requisitos específicos de rendimiento, carga, escalabilidad y seguridad.
>
>>Consulte también la página [requisitos técnicos](/help/sites-deploying/technical-requirements.md#supported-platforms).

### Búsqueda {#search-features}

En esta sección se enumeran los proveedores de índices personalizados utilizados con AEM. Para obtener más información acerca de la indexación, consulte [Consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Para la mayoría de las implementaciones, Adobe recomienda utilizar el índice Lucene. Utilice Solr únicamente para la escalabilidad en implementaciones especializadas y complejas.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Directrices de desarrollo {#development-guidelines}

Desarrollo para AEM con el objetivo de **rendimiento y escalabilidad**. Las siguientes son prácticas recomendadas que puede seguir:

**HACER**

* Aplicar la separación de presentación, lógica y contenido
* Utilice las API de AEM existentes (por ejemplo, Sling) y las herramientas (por ejemplo, Replication)
* Desarrollar en el contexto de contenido real
* Desarrollar para lograr una caché óptima
* Minimizar el número de guardados (por ejemplo, mediante flujos de trabajo transitorios)
* Asegúrese de que todos los puntos finales HTTP sean RESTful
* Restringir el ámbito de la observación JCR
* Tenga en cuenta el subproceso asincrónico

**NO SE**

* No utilice directamente las API de JCR, si es posible
* No cambie /libs, sino que utilice superposiciones
* No utilice consultas siempre que sea posible
* No utilice enlaces de Sling para obtener servicios OSGi en código Java™, sino que utilice:

   * @Reference en un componente DS
   * @Inject en un modelo Sling
   * sling.getService() en una clase de uso de Sightly
   * sling.getService() en un JSP
   * un ServiceTracker
   * acceso directo al registro de servicios OSGi

Para obtener más información sobre el desarrollo en AEM, lea [Desarrollo: Conceptos básicos](/help/sites-developing/the-basics.md). Para ver prácticas recomendadas adicionales, consulte [Prácticas recomendadas de desarrollo](/help/sites-developing/best-practices.md).

### Escenarios de referencia {#benchmark-scenarios}

>[!NOTE]
>
>Todas las pruebas de referencia mostradas en esta página se han realizado en un entorno de laboratorio.

Los escenarios de prueba detallados a continuación se utilizan para las secciones de referencia de los capítulos TarMK, MongoMk y TarMK vs MongoMk. Para ver qué escenario se utilizó para una prueba de referencia determinada, lea el campo Escenario de la tabla [Especificaciones técnicas](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark).

**Escenario de un solo producto**

AEM Assets:

* Interacciones del usuario: Examinar Assets/Buscar Assets/Descargar recurso/Leer metadatos del recurso/Actualizar metadatos del recurso/Cargar recurso/Ejecutar flujo de trabajo de cargar recurso
* Modo de ejecución: usuarios simultáneos, una sola interacción por usuario

**Escenario de mezcla de productos**

AEM Sites + Assets:

* Interacciones de usuario de Sites: Leer página de artículo/Leer página/Crear párrafo/Editar párrafo/Crear página de contenido/Activar página de contenido/Búsqueda de autor
* Interacciones del usuario de Assets: Examinar Assets/Buscar Assets/Descargar recurso/Leer metadatos del recurso/Actualizar metadatos del recurso/Cargar recurso/Ejecutar flujo de trabajo de cargar recurso
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

**Escenario de caso de uso vertical**

Medios:

* `Read Article Page (27.4%), Read Page (10.9%), Create Session (2.6%), Activate Content Page (1.7%), Create Content Page (0.4%), Create Paragraph (4.3%), Edit Paragraph (0.9%), Image Component (0.9%), Browse Assets (20%), Read Asset Metadata (8.5%), Download Asset (4.2%), Search Asset (0.2%), Update Asset Metadata (2.4%), Upload Asset (1.2%), Browse Project (4.9%), Read Project (6.6%), Project Add Asset (1.2%), Project Add Site (1.2%), Create Project (0.1%), Author Search (0.4%)`
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

## TarMK {#tarmk}

Este capítulo proporciona directrices generales de rendimiento para TarMK que especifican los requisitos mínimos de arquitectura y la configuración. También se proporcionan pruebas de referencia para una mayor aclaración.

Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de autor de AEM como para las de publicación.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento Tar](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Directrices de arquitectura mínima de TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>Las directrices de arquitectura mínimas que se presentan a continuación son para entornos de producción y sitios con alto tráfico. Estas pautas son **no** las [especificaciones mínimas](/help/sites-deploying/technical-requirements.md#prerequisites) para ejecutar AEM.

Para establecer un buen rendimiento al usar TarMK, debe comenzar desde la siguiente arquitectura:

* Una instancia de autor
* Dos instancias de publicación
* Dos Dispatcher

A continuación se muestran las directrices arquitectónicas para los sitios y AEM Assets de AEM.

>[!NOTE]
>
>La replicación sin binarios debe activarse **ON** si se comparte el almacén de datos de archivos.

**Directrices de arquitectura Tar para AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Directrices de arquitectura Tar para AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Directrices de configuración de TarMK {#tarmk-settings-guideline}

Para obtener un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, consulte [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajos de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitorio de Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> </td>
   <td>Para evitar que las consultas expansivas se sobrecarguen en los sistemas, añada estos parámetros JVM en el script de inicio de AEM.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Habilitado</p> <p>Habilitado</p> <p>Habilitado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo de la pila</p> </td>
   <td>Consulte también <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configuraciones de almacén de datos</a>.</td>
  </tr>
  <tr>
   <td>Flujo de trabajo de recursos de actualización DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>activado</td>
   <td>Este flujo de trabajo administra la actualización de recursos.</td>
  </tr>
  <tr>
   <td>Reescritura de metadatos DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>activado</td>
   <td>Este flujo de trabajo administra la reescritura de XMP al binario original y establece la fecha de la última modificación en JCR.</td>
  </tr>
 </tbody>
</table>

### Referencia de rendimiento de TarMK {#tarmk-performance-benchmark}

#### Especificaciones técnicas {#technical-specifications}

Los ensayos de referencia se realizaron con arreglo a las siguientes especificaciones:

| | **Nodo de autor** |
|---|---|
| Servidor | Hardware de metal desnudo (HP) |
| Sistema operativo | Red Hat® Linux® |
| CPU/Núcleos | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 núcleos |
| RAM | 32 GB |
| Disco | Magnético |
| Java™ | Oracle JRE versión 8 |
| Montón de JVM | 16 GB |
| Producto | AEM 6.2 |
| Nodestore | TarMK |
| Almacén de datos | DS de archivo |
| Escenario | Un solo producto: Assets / 30 hilos simultáneos |

#### Resultados de referencia de rendimiento {#performance-benchmark-results}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son los números de rendimiento real.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

La razón principal para elegir el backend de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esta capacidad significa tener dos o más instancias de autor activas siempre en ejecución y utilizar MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe generalmente al hecho de que la capacidad de CPU y de memoria de un solo servidor, que admite todas las actividades de creación simultáneas, ya no es sostenible.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento de Mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Directrices de arquitectura mínima de MongoMK {#mongomk-minimum-architecture-guidelines}

Para establecer un buen rendimiento al utilizar MongoMK, debe comenzar desde la siguiente arquitectura:

* Tres instancias de autor
* Dos instancias de publicación
* Tres instancias de MongoDB
* Dos Dispatcher

>[!NOTE]
>
>En entornos de producción, MongoDB siempre se utiliza como un conjunto de réplicas con un principal y dos secundarios. Las lecturas y escrituras van a la primaria y las lecturas pueden ir a la secundaria. Si el almacenamiento no está disponible, uno de los secundarios se puede reemplazar por un árbitro, pero los conjuntos de réplicas de MongoDB siempre deben estar compuestos por un número impar de instancias.

>[!NOTE]
>
>La replicación sin binarios debe activarse **ON** si se comparte el almacén de datos de archivos.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Directrices de configuración de MongoMK {#mongomk-settings-guidelines}

Para obtener un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, consulte [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Valor (predeterminado)</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajos de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitorio de Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> <p>60000</p> </td>
   <td>Para evitar que las consultas expansivas se sobrecarguen en los sistemas, añada estos parámetros JVM en el script de inicio de AEM.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Habilitado</p> <p>Habilitado</p> <p>Habilitado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo de la pila</p> </td>
   <td>Consulte también <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configuraciones de almacén de datos</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>El tamaño predeterminado de la caché se establece en 256 MB.</p> <p>Afecta al tiempo que se tarda en realizar la invalidación de la caché.</p> </td>
  </tr>
  <tr>
   <td>oak-observación</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>mín. y máx. = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Análisis de rendimiento de MongoMK {#mongomk-performance-benchmark}

### Especificaciones técnicas {#technical-specifications-1}

Los ensayos de referencia se realizaron con arreglo a las siguientes especificaciones:

| | **Nodo de autor** | **Nodo MongoDB** |
|---|---|---|
| Servidor | Hardware de metal desnudo (HP) | Hardware de metal desnudo (HP) |
| Sistema operativo | Red Hat® Linux® | Red Hat® Linux® |
| CPU/Núcleos | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 núcleos | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 núcleos |
| RAM | 32 GB | 32 GB |
| Disco | Magnético: >1.000 IOPS | Magnético: >1.000 IOPS |
| Java™ | Oracle JRE versión 8 | N/D |
| Montón de JVM | 16 GB | N/D |
| Producto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/D |
| Almacén de datos | DS de archivo | N/D |
| Escenario | Un solo producto: Assets / 30 hilos simultáneos | Un solo producto: Assets / 30 hilos simultáneos |

### Resultados de referencia de rendimiento {#performance-benchmark-results-1}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son los números de rendimiento real.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

La regla básica a tener en cuenta al elegir entre los dos es que TarMK está diseñado para el rendimiento, mientras que MongoMK se utiliza para la escalabilidad. Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de autor de AEM como para las de publicación.

La razón principal para elegir el backend de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esta funcionalidad significa tener dos o más instancias de autor activas siempre en ejecución y utilizar MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe generalmente al hecho de que la capacidad de CPU y de memoria de un solo servidor, que admite todas las actividades de creación simultáneas, ya no es sostenible.

Para obtener más información sobre TarMK y MongoMK, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Directrices TarMK vs MongoMk {#tarmk-vs-mongomk-guidelines}

**Ventajas de TarMK**

* Creado específicamente para aplicaciones de gestión de contenido
* Los archivos siempre son coherentes y se pueden realizar copias de seguridad utilizando cualquier herramienta de copia de seguridad basada en archivos
* Proporciona un mecanismo de conmutación por error: consulte [Suspensión en frío](/help/sites-deploying/tarmk-cold-standby.md) para obtener más información
* Proporciona un alto rendimiento y un almacenamiento de datos fiable con una sobrecarga operativa mínima
* Menor coste total de propiedad (TCO)

**Criterios para elegir MongoMK**

* Número de usuarios con nombre conectados en un día: en miles o más
* Número de usuarios simultáneos: en cientos o más
* Volumen de ingestas de recursos por día: en cientos de miles o más
* Volumen de ediciones de página al día: en cientos de miles o más
* Volumen de búsquedas por día: en decenas de miles o más

### Puntos de referencia de TarMK vs MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son números de rendimiento real.

### Especificaciones técnicas del escenario 1 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo OAK de autor</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>Hardware de metal desnudo (HP)</td>
   <td>Hardware de metal desnudo (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/Núcleos</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 núcleos</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 núcleos</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>Magnético: &gt;1.000 IOPS</td>
   <td>Magnético: &gt;1.000 IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE versión 8</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Montón de JVM16 GB</td>
   <td>16 GB</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Producto </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK o MongoMK</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Almacén de datos</td>
   <td>DS de archivo </td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> Un solo producto: Assets / 30 hilos simultáneos por ejecución</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resultados de referencia de rendimiento del escenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Especificaciones técnicas del escenario 2 {#scenario-technical-specifications-1}

>[!NOTE]
>
>Para habilitar el mismo número de autores con MongoDB que con un sistema TarMK, necesita un clúster con dos nodos de AEM. Un clúster MongoDB de cuatro nodos puede administrar 1,8 veces el número de autores que una instancia de TarMK. Un clúster de MongoDB de ocho nodos puede administrar 2,3 veces el número de autores que una instancia de TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo TarMK de autor</strong></td>
   <td><strong>Nodo MongoMK de autor</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
  </tr>
  <tr>
   <td>CPU/Núcleos</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60 GB</td>
   <td>60 GB</td>
   <td>60 GB</td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>SSD: 10.000 IOPS</td>
   <td>SSD: 10.000 IOPS</td>
   <td>SSD: 10.000 IOPS</td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE versión 8</td>
   <td><br /> Oracle JRE versión 8</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Montón de JVM16 GB</td>
   <td>30 GB</td>
   <td>30 GB</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Producto </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Almacén de datos</td>
   <td>DS de archivo </td>
   <td><br /> DS de archivo</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> <br /> Caso de uso vertical: Media / 2000 subprocesos simultáneos</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Resultados de referencia de rendimiento del escenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Directrices de escalabilidad de arquitectura para AEM Sites y Assets {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Resumen de las directrices de rendimiento  {#summary-of-performance-guidelines}

Las directrices presentadas en esta página se pueden resumir de la siguiente manera:

* **TarMK con almacén de datos de archivos** - La arquitectura recomendada para la mayoría de los clientes:

   * Topología mínima: una instancia de autor, dos instancias de publicación, dos instancias de Dispatcher
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **MongoMK con almacén de datos de archivos** - La arquitectura recomendada para la escalabilidad horizontal del nivel de Author:

   * Topología mínima: tres instancias de autor, tres instancias de MongoDB, dos instancias de publicación, dos instancias de Dispatcher
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **Nodestore**: almacenado en el disco local, no en un almacenamiento conectado a la red (NAS)
* Al usar **Amazon S3**:

   * El almacén de datos de Amazon S3 se comparte entre los niveles Author y Publish
   * La replicación sin binarios debe estar activada
   * La recolección de elementos no utilizados del almacén de datos requiere una primera ejecución en todos los nodos de autor y publicación y, a continuación, una segunda ejecución en autor

* **Se debe crear un índice personalizado además del índice predeterminado**, basado en las búsquedas más comunes

   * Los índices de Lucene deben utilizarse para los índices personalizados

* **La personalización del flujo de trabajo puede mejorar considerablemente el rendimiento**: elimine el paso de vídeo del flujo de trabajo &quot;Actualizar recurso&quot;, deshabilite los agentes de escucha que no se usen, etc.

Para obtener más información, lea también la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).
