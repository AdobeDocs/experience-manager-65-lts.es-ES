---
title: Conceptos básicos de configuración
description: Aprenda a configurar Adobe Experience Manager para sus propios requisitos específicos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 338ea82e-c248-4118-9d42-e268d6396e65
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2093'
ht-degree: 0%

---

# Conceptos básicos de configuración{#basic-configuration-concepts}

Adobe Experience Manager (AEM) se instala con la configuración predeterminada de todos los parámetros, lo que le permite ejecutarse de forma predeterminada. Sin embargo, puede configurar AEM para sus propios requisitos específicos.

Hay muchos aspectos de AEM que se pueden configurar:

* Algunos están [configurados comúnmente para cada instalación de proyecto](#primary-configuration-considerations) y deben revisarse para confirmar si son aplicables a su proyecto.
* [Otras configuraciones](#further-configuration-considerations) pueden ser comunes pero no imperativas; están relacionadas con características o con el rendimiento y la estabilidad del sistema.
* Otras solo son necesarias para determinadas funciones opcionales de AEM (se documentan junto con la función adecuada).

Según la configuración específica, estos cambios se pueden realizar mediante las siguientes opciones:

* **Consola web de Adobe CQ**

  Esta es una ubicación estándar para configurar paquetes y servicios de OSGi.

  Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y prácticas recomendadas.

* **Repositorio**

  Hay un subconjunto de configuraciones de OSGi disponibles en el repositorio. Esto garantiza que al copiar o replicar el contenido del repositorio se vuelvan a crear configuraciones idénticas. También puede agregar sus propias configuraciones, según el modo de ejecución, al repositorio.

  Consulte la configuración de [OSGi en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) y, en particular, [Agregar una nueva configuración al repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obtener más información.

* **Sistema de archivos**

  Algunos archivos de configuración residen en el sistema de archivos.

* **WCM DE AEM**

  Se pueden configurar varios aspectos dentro del propio WCM de AEM, muchos de los cuales utilizan la consola [Tools](/help/sites-administering/tools-consoles.md); por ejemplo, los agentes de replicación.

>[!NOTE]
>
>Al trabajar con Adobe Experience Manager, existen varios métodos para administrar los ajustes de configuración de los servicios OSGi (nodos de consola o de repositorio).
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

>[!NOTE]
>
>La configuración de AEM es sencilla. Sin embargo, ciertos cambios pueden tener un impacto importante en las aplicaciones. Por este motivo, asegúrese de que tiene la experiencia y los conocimientos necesarios antes de empezar a configurar AEM y realice solo los cambios que sepa que son necesarios. Cualquier cambio realizado a través de la consola OSGi se aplica **inmediatamente** al sistema en ejecución (no se requiere reiniciar).

## Consideraciones de configuración principal {#primary-configuration-considerations}

Esta lista detalla las áreas principales que se configuran comúnmente para cada nuevo proyecto. No todos son necesarios, pero la lista debe leerse y revisarse para ver qué es aplicable a su proyecto.

La lista proporciona una breve descripción de cada aspecto de la configuración, junto con vínculos a las páginas que proporcionan detalles completos.

### Lista de comprobación de seguridad {#security-checklist}

Hay varios problemas de configuración clave en la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md). Asegúrese de leer esto y de realizar las acciones necesarias para la instalación.

### Configuración de la interfaz de usuario predeterminada: táctil o clásica {#configuring-the-default-ui-touch-optimized-or-classic}

Hay dos interfaces de usuario disponibles para usar en AEM:

* La IU táctil optimizada
* La IU clásica

Puede configurar la interfaz de usuario que necesite mediante [Asignación raíz](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Encontrará más información sobre cómo seleccionar la interfaz de usuario en [Selección de la interfaz de usuario](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de AEM (por ejemplo, el repositorio y Dispatcher) se pueden instalar en redes IPv4 e IPv6.

El funcionamiento es fluido, ya que no se requiere ninguna configuración especial; cuando sea necesario, simplemente puede especificar una dirección IP utilizando el formato adecuado para su tipo de red.

Esto significa que cuando se debe especificar una dirección IP, se puede seleccionar (según sea necesario) entre:

* una dirección IPv6

  por ejemplo, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* una dirección IPv4

  por ejemplo, `https://123.1.1.4:4502`

* un nombre de servidor

  por ejemplo, `https://www.yourserver.com:4502`

* el caso predeterminado de `localhost` se interpretará para las instalaciones de red IPv4 e IPv6

  por ejemplo, `http://localhost:4502`

### Depuración de versiones {#version-purging}

En una instalación estándar, AEM crea una versión de una página o nodo cada vez que activa una página (después de actualizar el contenido). También puede crear versiones adicionales si lo solicita usando la ficha **Creación de versiones** de la barra de tareas. Todas estas versiones se almacenan en el repositorio y se pueden restaurar, si es necesario.

Estas versiones nunca se depuran, por lo que el tamaño del repositorio aumenta con el tiempo y, por lo tanto, debe administrarse.

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener información detallada, en particular [Administrador de versiones](/help/sites-deploying/version-purging.md#version-manager) para saber cómo configurar AEM para purgar versiones anteriores cuando se crea una nueva versión.

### Registro {#logging}

AEM permite configurar lo siguiente:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para solicitar información
* configuración específica para los servicios individuales; por ejemplo, un archivo de registro individual y formato para los mensajes de registro

Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener información detallada.

### Ejecutar modos {#run-modes}

Los modos de ejecución permiten ajustar la instancia de AEM para un propósito específico. Por ejemplo, crear o publicar, probar, desarrollar o intranet, etc.

Esto se realiza definiendo colecciones de parámetros de configuración para cada modo de ejecución. Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución y, a continuación, puede ajustar conjuntos adicionales para el propósito de su entorno específico. A continuación, se aplican según sea necesario.

Todas las opciones de configuración se almacenan en el único repositorio y se activan al establecer el **Modo de ejecución**.

Consulte [Modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener información detallada.

### Inicio de sesión único {#single-sign-on}

Inicio de sesión único (SSO) permite a un usuario acceder a varios sistemas después de proporcionar credenciales de autenticación (como nombre de usuario y contraseña) una vez. Un sistema independiente (conocido como autenticador de confianza) realiza la autenticación y proporciona a Experience Manager las credenciales de usuario. Experience Manager comprueba y aplica los permisos de acceso del usuario (es decir, determina a qué recursos puede acceder el usuario).

Consulte [Inicio de sesión único](/help/sites-deploying/single-sign-on.md) para obtener más información.

### Asignación de recursos {#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, URL de vanidad y hosts virtuales para AEM.

Por ejemplo, puede utilizar estas asignaciones para lo siguiente:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a la página `/content/en/gateway` de su sitio web se redirijan a `https://gbiv.com/`.

Consulte [Asignación de recursos](/help/sites-deploying/resource-mapping.md) para obtener más información.

### Agentes de replicación, replicación inversa y replicación {#replication-reverse-replication-and-replication-agents}

Los agentes de replicación son fundamentales para AEM como mecanismo para lo siguiente:

* [Publicar (activar)](/help/sites-authoring/publishing-pages.md) contenido de un autor en un entorno de publicación.
* Vaciar explícitamente el contenido de la caché de Dispatcher.
* Devolver los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) desde el entorno de publicación al entorno de creación (bajo el control del entorno de creación).

Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).

### Ajustes de configuración de OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) es un elemento fundamental en la pila de tecnología de AEM. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

Consulte [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener una lista de los distintos paquetes que son relevantes para la implementación del proyecto (enumerados según el paquete). No es necesario ajustar todas las configuraciones enumeradas, algunas se mencionan para ayudarle a comprender cómo funciona AEM.

Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

### Configuración de LDAP {#configuring-ldap}

Se requiere autenticación LDAP para autenticar a los usuarios almacenados en un directorio LDAP (central) como Active Directory. Esto ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario.

La autenticación LDAP se produce en el nivel del repositorio, por lo que el repositorio la gestiona directamente. Para obtener más información, consulte [Configuración de LDAP con AEM](/help/sites-administering/ldap-config.md).

Para administrar usuarios en AEM (incluida la asignación de derechos de acceso), consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

### Configuración de Dispatcher {#configuring-the-dispatcher}

Dispatcher es la herramienta de Adobe Experience Manager para el almacenamiento en caché, el equilibrio de carga o ambos. Se puede utilizar con un servidor web de clase empresarial.

Consulte [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para obtener información detallada, en particular [Configuración de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html) para obtener más información sobre la configuración.

### Configuración del conector de AEM LiveCycle {#configuring-aem-livecycle-connector}

Con el lanzamiento de AEM Doc Services y AEM Doc Security, AEM ahora tiene la capacidad de invocar los servicios de documento de LiveCycle para procesar un formulario XFA, convertir un documento en PDF y proteger un documento mediante políticas. Consulte [Conector de AEM LiveCycle](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) para obtener más información.

### Administración de topologías y descarga de trabajos {#job-offloading-and-topology-administration}

[La descarga](/help/sites-deploying/offloading.md) distribuye las tareas de procesamiento entre las instancias de Experience Manager de una topología. Con la descarga, puede utilizar instancias de Experience Manager específicas para realizar tipos específicos de procesamiento. El procesamiento especializado le permite maximizar el uso de los recursos de servidor disponibles.

Las topologías son clústeres de Experience Manager de correspondencia imprecisa que participan en la descarga. Un clúster consta de una o más instancias de servidor de Experience Manager (una sola instancia se considera un clúster).

Para obtener más información sobre cómo ver o modificar la pertenencia a la topología, consulte la sección [Administración de topologías](/help/sites-deploying/offloading.md#administering-topologies).

### Configuración de la consola de bienvenida {#configuring-the-welcome-console}

La consola de bienvenida de la IU clásica proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM.

Es posible configurar los vínculos visibles; consulte [Configuración de la consola de bienvenida](/help/sites-developing/customizing-the-welcome-console.md) para obtener más información.

### Configurar para el rendimiento {#configuring-for-performance}

[El rendimiento](/help/sites-deploying/configuring-performance.md) es clave para tu proyecto. Se pueden configurar ciertos aspectos de AEM (o del repositorio subyacente) para optimizar el rendimiento.

Consulte [Configuración del rendimiento](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obtener más información.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Almacén de datos compartidos {#shared-data-store}

El almacén de datos del repositorio se utiliza para descargar el almacenamiento de binarios grandes del repositorio en un área separada, de modo que varias instancias del mismo binario (una imagen, por ejemplo) dentro del árbol del repositorio se almacenen solo una vez.

Esta función &quot;almacenar una vez, hacer referencia varias veces&quot; se puede ampliar para que sirva no solo a un único árbol de repositorios, sino a repositorios completamente independientes, configurando el almacén de datos de cada uno para hacer referencia a la misma ubicación del sistema de archivos compartido.

Este almacén de datos se puede compartir entre diferentes nodos del mismo clúster, diferentes instancias de publicación o autor en la misma instalación o incluso instancias totalmente independientes en diferentes instalaciones.

Para obtener más información, consulte [Configuración de almacenes de datos y almacenes de nodos](/help/sites-deploying/data-store-config.md).

## Consideraciones de configuración adicionales {#further-configuration-considerations}

### Habilitar HTTP sobre SSL {#enabling-http-over-ssl}

Puede habilitar HTTP sobre SSL para utilizar conexiones más seguras con sus servidores.

Consulte [Habilitación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### Portales y portlets de AEM {#aem-portals-and-portlets}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido desde diferentes fuentes y aloja la capa de presentación de los sistemas de información. El componente portlet también permite incrustar un portlet en la página. Para acceder al contenido proporcionado por CQ5 WCM, el servidor de portal se puede acoplar al portlet CQ5 Portal Director. Para ello, instale, configure y agregue el portlet a la página del portal.

Consulte [Portal y portlets](/help/sites-administering/aem-as-portal.md) para obtener más información.

### Caducidad de objetos estáticos {#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, los iconos) no cambian. Por lo tanto, el sistema debe configurarse para que no caduque (durante un periodo de tiempo razonable) y, por lo tanto, reducir el tráfico innecesario.

Consulte [Caducidad de objetos estáticos](/help/sites-deploying/expiration-static-objects.md) para obtener más información.

### Abrir archivos en el proceso de Java™ {#open-files-in-the-java-process}

Cada proceso de Java™ puede acceder a los archivos; esto requiere recursos del sistema. Por este motivo, se define un límite superior en cuanto a la cantidad de archivos a los que puede acceder cada proceso de forma simultánea. Si se supera este límite, puede producirse un error de excepción.

Si el proceso de AEM supera este máximo, se verá el mensaje &quot;`too many open files`&quot; en `error.log`.

Para evitar estas excepciones, haga lo siguiente:

1. Compruebe cuántos archivos abiertos está utilizando el proceso de AEM.

   Esta comprobación depende de la plataforma en la que se esté ejecutando la instancia. Se pueden utilizar utilidades como lsof (UNIX®) o Process Explorer (Windows).

   Este valor debe controlarse durante el desarrollo y las pruebas para:

   * confirme que los archivos se cierran según sea necesario
   * para determinar el valor máximo necesario (en diversas circunstancias)

1. Defina el máximo permitido.

   El nuevo valor debe satisfacer tanto las necesidades actuales como los picos futuros, por lo que es aconsejable duplicar las necesidades actuales.

   De manera predeterminada, `serverctl` configura `CQ_MAX_OPEN_FILES` en `8192`; esto debería ser suficiente para la mayoría de los escenarios.

### Configuración del editor de texto enriquecido {#configuring-the-rich-text-editor}

El **Editor de texto enriquecido** (**RTE**) proporciona a los autores una amplia gama de [funciones](/help/sites-authoring/rich-text-editor.md) para editar su contenido textual; proporcionándoles iconos, cuadros de selección y menús para una experiencia WYSIWYG.

Consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md) para obtener más información.

### Configurar Deshacer para editar páginas {#configuring-undo-for-page-editing}

Existen varias propiedades que controlan el comportamiento de los comandos Deshacer y Rehacer para editar páginas. Se pueden configurar, consulte [Configuración de Deshacer para la edición de páginas](/help/sites-administering/config-undo.md) para obtener más información.

### Configuración del componente de vídeo {#configuring-the-video-component}

El [componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) le permite colocar un elemento de vídeo predefinido y listo para usar en su página.

Para que se produzca la transcodificación adecuada, el administrador debe [Instalar FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) por separado. También pueden [Configurar los perfiles de vídeo](/help/sites-administering/config-video.md#configure-video-profiles) para usarlos con elementos html5.

### Configuración y personalización de informes {#configuring-and-customizing-reports}

Para ayudarle a monitorizar y analizar el estado de su instancia, CQ proporciona una selección de informes predeterminados, que se pueden configurar para sus necesidades individuales:

Consulte los [Conceptos básicos de la personalización de informes](/help/sites-administering/reporting.md#the-basics-of-report-customization) para obtener más información.

### Configuración de notificaciones por correo electrónico {#configuring-email-notification}

CQ envía notificaciones por correo electrónico a los usuarios que:

* Se han suscrito a eventos de página como, por ejemplo, modificaciones o replicaciones.
* Se ha suscrito a eventos de foro.
* Deben realizar un paso en un flujo de trabajo.

Consulte [Configuración de la notificación por correo electrónico](/help/sites-administering/notification.md) para obtener más información.

### Habilitando impresiones de página {#enabling-page-impressions}

Las impresiones de página se muestran en la columna **Impresiones** de la consola siteadmin de la IU clásica. Para habilitar la captura de impresiones de página, configure lo siguiente:

* En la instancia de publicación:

   * [Estadísticas de página de CQ WCM de día](/help/sites-deploying/osgi-configuration-settings.md)

* En la instancia de autor:

   * [Rastreador de impresiones de página de Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuración del Rastreador de impresiones de página de Adobe en el entorno de creación permite las solicitudes anónimas al servicio de seguimiento.
