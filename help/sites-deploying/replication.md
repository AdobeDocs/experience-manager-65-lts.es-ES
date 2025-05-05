---
title: Replicación
description: Obtenga información sobre cómo configurar y supervisar agentes de replicación en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b840d970-9365-4df3-8467-e34abd940074
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '3270'
ht-degree: 1%

---

# Replicación{#replication}

Los agentes de replicación son fundamentales para Adobe Experience Manager (AEM) como mecanismo utilizado para lo siguiente:

* [Publicar (activar)](/help/sites-authoring/publishing-pages.md#activatingcontent) contenido de un autor en un entorno de publicación.
* Vaciar explícitamente el contenido de la caché de Dispatcher.
* Devolver los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) desde el entorno de publicación al entorno de creación (bajo el control del entorno de creación ).

Las solicitudes están [en cola](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) para que las procese el agente apropiado.

>[!NOTE]
>
>Los datos de usuario (usuarios, grupos de usuarios y perfiles de usuario) no se replican entre instancias de autor y publicación.
>
>Para varias instancias de publicación, los datos de usuario se distribuyen mediante Sling cuando la [sincronización de usuarios](/help/sites-administering/sync.md) está habilitada.

## Duplicación de autor a publicación {#replicating-from-author-to-publish}

La replicación, en una instancia de publicación o Dispatcher, se realiza en varios pasos:

* el autor solicita que se publique determinado contenido (activado); esto se puede iniciar mediante una solicitud manual o mediante déclencheur automáticos que se han preconfigurado.
* la solicitud se pasa al agente de replicación predeterminado adecuado; un entorno puede tener varios agentes predeterminados que siempre están seleccionados para este tipo de acciones.
* el agente de replicación &quot;empaqueta&quot; el contenido y lo coloca en la cola de replicación.
* en la ficha Sitios web, el [indicador de estado de color](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) está establecido para las páginas individuales.
* el contenido se elimina de la cola y se transporta al entorno de publicación mediante el protocolo configurado; normalmente es HTTP.
* un servlet en el entorno Publish recibe la solicitud y publica el contenido recibido; el servlet predeterminado es `https://localhost:4503/bin/receive`.

* se pueden configurar varios entornos Author y Publish.

![chlimage_1-21](assets/chlimage_1-21.png)

### Duplicación desde Publicar en Autor {#replicating-from-publish-to-author}

Algunas funciones permiten a los usuarios introducir datos en una instancia de publicación.

A veces, se necesita un tipo de replicación conocido como replicación inversa para devolver estos datos al entorno de Author desde el que se redistribuyen a otros entornos de publicación. Debido a consideraciones de seguridad, cualquier tráfico del entorno de publicación al de creación debe estar estrictamente controlado.

La replicación inversa utiliza un agente en el entorno de publicación que hace referencia al entorno de creación. Este agente coloca los datos en una bandeja de salida. Esta bandeja de salida coincide con los oyentes de replicación en el entorno de creación. Los oyentes sondean las bandejas de salida para recopilar los datos introducidos y luego distribuirlos según sea necesario. Esto garantiza que el entorno de creación controle todo el tráfico.

### Replicación: de forma predeterminada {#replication-out-of-the-box}

Cree una página siguiendo [Creación y organización de páginas](/help/sites-authoring/managing-pages.md).

Para seguir este ejemplo y usar los agentes de replicación predeterminados, [instale AEM](/help/sites-deploying/deploy.md) con:


* el entorno de creación en el puerto `4502`
* el entorno de publicación en el puerto `4503`

Esta replicación se lleva a cabo desde el entorno de creación mediante:

* **Agente predeterminado (publicar)**
Este agente replica el contenido en la instancia de publicación predeterminada.
Se puede acceder a los detalles de esto (configuración y registros) desde la consola Herramientas del entorno de creación; o bien:
  `http://localhost:4502/etc/replication/agents.author/publish.html`.

>[!NOTE]
>
>Habilitado de forma predeterminada:
>
>* Agentes en Autor : Agente predeterminado (publicar); si no es así, asegúrese de habilitarlo antes de continuar.
>
>Deshabilitado de forma predeterminada (a partir de AEM 6.1):
>
>* Agentes en Autor : Agente de replicación inversa (publish_reverse)
>* Agentes en publicación: replicación inversa (bandeja de salida)
>
>Para comprobar el estado del agente o de la cola, use la consola **Herramientas**.
>Consulte [Supervisión de los agentes de replicación](#monitoring-your-replication-agents).

#### Replicación (de autor a publicación) {#replication-author-to-publish}

1. Vaya a la página de asistencia técnica en el entorno de creación.
   **https://localhost:4502/content/site1/test.html** `<pi>`
1. Edite la página para poder agregar texto nuevo.
1. **Activar página** para poder publicar los cambios.
1. Abra la página de soporte en el entorno de publicación:
   **https://localhost:4503/content/site1/test.html**
1. Ahora puede ver los cambios introducidos en Autor.


#### Agentes de replicación: predefinidos {#replication-agents-out-of-the-box}

Los siguientes agentes están disponibles en una instalación estándar de AEM:

* [Agente predeterminado](#replication-author-to-publish)
Se utiliza para replicar de Autor a Publicar.

* Vaciado de Dispatcher
Se utiliza para administrar la caché de Dispatcher. Consulte [Invalidación de la caché de Dispatcher desde el entorno de creación](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es#invalidating-dispatcher-cache-from-the-authoring-environment) e [Invalidación de la caché de Dispatcher desde una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es#invalidating-dispatcher-cache-from-a-publishing-instance) para obtener más información.

* [Replicación inversa](#configuring-reverse-replication)
Se utiliza para replicar desde Publicar en Autor. La replicación inversa no se utiliza para funciones de Communities, como foros, blogs y comentarios. Se desactiva de forma efectiva, ya que la bandeja de salida no está activada. El uso de la replicación inversa requeriría una configuración personalizada.

* Agente estático
Se trata de un &quot;agente que almacena una representación estática de un nodo en el sistema de archivos&quot;.
Por ejemplo, con la configuración predeterminada, las páginas de contenido y los recursos DAM se almacenan en `/tmp`, ya sea como HTML o en el formato de recurso adecuado. Consulte las fichas `Settings` y `Rules` para obtener la configuración.
Esto se solicitó para que cuando la página se solicite directamente desde el servidor de aplicaciones, se pueda ver el contenido. Es un agente especializado y (probablemente) no es necesario en la mayoría de los casos.

## Agentes de replicación: parámetros de configuración {#replication-agents-configuration-parameters}

Al configurar un agente de replicación desde la consola Herramientas, hay cuatro pestañas disponibles en el cuadro de diálogo:

### Configuración {#settings}

* **Nombre**

  Un nombre único para el agente de replicación.

* **Descripción**

  Una descripción del propósito que cumple este agente de replicación.

* **Habilitado**

  Indica si el agente de replicación está habilitado.

  Cuando el agente está **habilitado**, la cola se muestra de la siguiente manera:

   * **Activo** cuando los elementos se están procesando.
   * **Inactivo** cuando la cola está vacía.
   * **Bloqueado** cuando los elementos están en cola, pero no se pueden procesar; por ejemplo, cuando la cola de recepción está deshabilitada.

* **Tipo de serialización**

  El tipo de serialización:

   * **Predeterminado**: establezca si el agente se va a seleccionar automáticamente.
   * **Vaciado de Dispatcher**: seleccione esta opción si el agente se va a utilizar para vaciar la caché de Dispatcher.

* **Retraso de reintento**

  El retraso (tiempo de espera en milisegundos) entre dos reintentos, si se produce un problema.

  Predeterminado: `60000`

* **Id. de usuario agente**

  Según el entorno, el agente utiliza esta cuenta de usuario para:

   * recopilar y empaquetar el contenido del entorno de creación;
   * crear y escribir el contenido en el entorno de publicación

  Deje este campo vacío para utilizar la cuenta de usuario del sistema (la cuenta definida en sling como usuario administrador; de forma predeterminada es `admin`).

  >[!CAUTION]
  >
  >Para un agente en el entorno de creación, esta cuenta *debe* tener acceso de lectura a todas las rutas que desea replicar.

  >[!CAUTION]
  >
  >Para un agente en el entorno de publicación, esta cuenta *debe* tener el acceso de creación y escritura necesario para replicar el contenido.

  >[!NOTE]
  >
  >Esto se puede utilizar como mecanismo para seleccionar contenido específico para la replicación.

* **Nivel de registro**

  Especifica el nivel de detalle que se utilizará para los mensajes de registro.

   * `Error`: solo se registran errores
   * `Info`: se registran errores, advertencias y otros mensajes informativos
   * `Debug`: se utiliza un alto nivel de detalle en los mensajes, principalmente con fines de depuración

  Predeterminado: `Info`

* **Usar para replicación inversa**

  Indica si este agente se utiliza para la replicación inversa; devuelve los datos introducidos por el usuario desde el entorno Publicar en Autor.

* **Actualización de alias**

  Al seleccionar esta opción, se habilitan las solicitudes de invalidación de alias o de rutas de vanidad en Dispatcher. Consulte también [Configuración de un agente de vaciado de Dispatcher](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transporte {#transport}

* **URI**

  Esto especifica el servlet de recepción en la ubicación de destino. En particular, puede especificar el nombre de host (o alias) y la ruta de contexto a la instancia de destino aquí.

  Por ejemplo:

   * Un agente predeterminado puede replicarse en `https://localhost:4503/bin/receive`
   * Un agente de vaciado de Dispatcher puede replicarse en `https://localhost:8000/dispatcher/invalidate.cache`

  El protocolo especificado aquí (HTTP o HTTPS) determina el método de transporte.

  Para los agentes de vaciado de Dispatcher, la propiedad URI solo se utiliza si utiliza entradas de host virtual basadas en rutas para diferenciar entre granjas, utilice este campo para dirigirse a la granja para invalidarla. Por ejemplo, la granja n.º 1 tiene un host virtual de `www.mysite.com/path1/*` y la granja n.º 2 lo tiene de `www.mysite.com/path2/*`. Puede usar una dirección URL de `/path1/invalidate.cache` para dirigirse a la primera granja de servidores y `/path2/invalidate.cache` para dirigirse a la segunda.

* **Usuario**

  El nombre de usuario de la cuenta que se utilizará para acceder al destino.

* **Contraseña**

  Contraseña de la cuenta que se utilizará para acceder al destino.

* **Dominio NTLM**

  Dominio para autenticación NTML.

* **Host NTLM**

  Host para autenticación NTML.

* **Habilitar SSL relajado**

  Habilite esta opción si desea que se acepten certificados SSL de certificación propia.

* **Permitir certificados caducados**

  Habilite esta opción si desea que se acepten certificados SSL caducados.

#### Proxy {#proxy}

La siguiente configuración solo es necesaria si se necesita un proxy:

* **Host Proxy**

  Nombre de host del proxy utilizado para el transporte.

* **Puerto Proxy**

  Puerto del proxy.

* **Usuario Proxy**

  El nombre de usuario de la cuenta que se va a utilizar.

* **Contraseña de proxy**

  Contraseña de la cuenta que se va a utilizar.

* **Dominio NTLM de proxy**

  El dominio NTLM de proxy.

* **Host NTLM de proxy**

  El dominio NTLM de proxy.

#### Ampliado {#extended}

* **Interfaz**

  Aquí puede definir la interfaz de socket a la que desea enlazarse.

  Esto establece la dirección local que se utilizará al crear conexiones. Si no se establece, se utiliza la dirección predeterminada. Esto resulta útil para especificar la interfaz que se va a utilizar en sistemas de hosts múltiples o agrupados.

* **Método HTTP**

  El método HTTP que se va a utilizar.

  Para un agente de vaciado de Dispatcher, casi siempre es GET y no debe cambiarse (POST sería otro valor posible).

* **Encabezados HTTP**

  Se utilizan para los agentes de vaciado de Dispatcher y especifican los elementos que se deben vaciar.

  Para un agente de vaciado de Dispatcher, no debería ser necesario cambiar las tres entradas estándar:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  Se utilizan, según corresponda, para indicar la acción que se utilizará al vaciar el controlador o la ruta de acceso. Los subparámetros son dinámicos:

   * `{action}` indica una acción de replicación

   * `{path}` indica una ruta

  Se sustituyen por la ruta/acción relevante para la solicitud y, por lo tanto, no necesitan estar &quot;codificadas&quot;:

  >[!NOTE]
  >
  >Si ha instalado AEM en un contexto distinto del contexto predeterminado recomendado, debe registrar el contexto en los encabezados HTTP. Por ejemplo:
  >`CQ-Handle:/<*yourContext*>{path}`

* **Cerrar conexión**

  Habilite para poder cerrar la conexión después de cada solicitud.

* **Tiempo de espera de conexión**

  Tiempo de espera (en milisegundos) que se aplicará al intentar establecer una conexión.

* **Tiempo de espera de socket**

  Tiempo de espera (en milisegundos) que se aplicará mientras se espera el tráfico una vez establecida la conexión.

* **Versión de protocolo**

  Versión del protocolo. Por ejemplo, `1.0` para HTTP/1.0.

#### Activadores {#triggers}

Esta configuración se utiliza para definir déclencheur para la replicación automatizada:

* **Ignorar predeterminado**

  Si se selecciona, el agente se excluye de la replicación predeterminada; esto significa que no se utiliza si un autor de contenido emite una acción de replicación.

* **En la modificación**

  Aquí se activa automáticamente una replicación por parte de este agente cuando se modifica una página. Se utiliza para agentes de vaciado de Dispatcher, pero también para la replicación inversa.

* **En distribución**

  Si se selecciona, el agente replicará automáticamente cualquier contenido que esté marcado para su distribución cuando se modifique.

* **Tiempo de activación/desactivación alcanzado**

  Esto déclencheur la replicación automática (para activar o desactivar una página según corresponda) cuando se producen los tiempos de activación o desactivación definidos para una página. Se utiliza principalmente para agentes de vaciado de Dispatcher.

* **Al recibir**

  Si se selecciona, las cadenas de agentes se replican cada vez que reciben eventos de replicación.

* **Sin actualización de estado**

  Cuando se selecciona, el agente no fuerza una actualización del estado de replicación.

* **Sin versiones**

  Cuando se selecciona, el agente no fuerza la creación de versiones de páginas activadas.

## Configuración de los agentes de replicación {#configuring-your-replication-agents}

### Configuración de los agentes de replicación desde el entorno de creación {#configuring-your-replication-agents-from-the-author-environment}

Desde la pestaña Herramientas del entorno de creación, puede configurar los agentes de replicación que residen en el entorno de creación (**Agentes de autor**) o en el entorno de publicación (**Agentes de publicación**). Los siguientes procedimientos ilustran la configuración de un agente para el entorno de creación, pero se pueden utilizar para ambos.

>[!NOTE]
>
>Cuando un Dispatcher administra solicitudes HTTP para instancias de autor o publicación, la solicitud HTTP del agente de replicación debe incluir el encabezado PATH. Además del siguiente procedimiento, debe agregar el encabezado PATH a la lista Dispatcher de encabezados de cliente. Consulte [/clientheaders (Client Headers)](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. Acceda a la ficha **Herramientas** en AEM.
1. Haga clic en **Replicación** (panel izquierdo para abrir la carpeta).
1. Haga doble clic en **Agentes de autor** (en el panel izquierdo o derecho).
1. Haga clic en el nombre del agente apropiado (que es un vínculo) para mostrar información detallada sobre ese agente.
1. Haga clic en **Editar** para que se abra el cuadro de diálogo de configuración:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Los valores proporcionados deberían ser suficientes para realizar una instalación predeterminada. Si realiza cambios, haga clic en **Aceptar** para guardarlos (consulte [Agentes de replicación - Parámetros de configuración](#replication-agents-configuration-parameters) para obtener información sobre parámetros individuales).

>[!NOTE]
>
>Una instalación estándar de AEM especifica `admin` como el usuario para las credenciales de transporte dentro de los agentes de replicación predeterminados.
>
>Esto debe cambiarse a una cuenta de usuario de replicación específica del sitio con los privilegios para replicar las rutas requeridas.

### Configuración de replicación inversa {#configuring-reverse-replication}

La replicación inversa se utiliza para devolver a una instancia de autor el contenido de usuario generado en una instancia de publicación. Esto se utiliza comúnmente para funciones como encuestas y formularios de registro.

Por razones de seguridad, la mayoría de las topologías de red no permiten conexiones *desde* la &quot;zona desmilitarizada&quot; (una subred que expone los servicios externos a una red que no es de confianza, como Internet).

Dado que el entorno de publicación suele estar en la DMZ, para devolver el contenido al entorno de creación, la conexión debe iniciarse desde la instancia de autor. Esto se realiza con:

* una *bandeja de salida* en el entorno de publicación donde se coloca el contenido.
* un agente (publicar) en el entorno de creación que sondea periódicamente la bandeja de salida en busca de contenido nuevo.

Para ello, necesita lo siguiente:

**Un agente de replicación inversa en el entorno de creación**. Actúa como componente activo para recopilar información de la bandeja de salida en el entorno de publicación:

Si desea utilizar la replicación inversa, asegúrese de que este agente está activado.

![chlimage_1-23](assets/chlimage_1-23.png)

**Un agente de replicación inversa en el entorno de publicación (una bandeja de salida)**: el elemento pasivo porque actúa como una &quot;bandeja de salida&quot;. La entrada del usuario se coloca aquí, desde donde la recopila el agente en el entorno de creación.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuración de la replicación para varias instancias de publicación {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Solo se replica el contenido: no se duplican los datos de usuario (usuarios, grupos de usuarios y perfiles de usuarios).
>
>Para sincronizar datos de usuario en varias instancias de publicación, habilite [Sincronización de usuarios](/help/sites-administering/sync.md).

Después de la instalación, ya se ha configurado un agente predeterminado para la replicación de contenido en una instancia de publicación que se ejecuta en el puerto 4503 del host local.

Para configurar la replicación de contenido para una instancia de publicación adicional, cree y configure un nuevo agente de replicación:

1. Abra la ficha **Herramientas** en AEM.
1. Seleccione **Replicación** y, a continuación, **Agentes de autor** en el panel izquierdo.
1. Seleccione **Nuevo...**.
1. Establezca **Title** y **Name**, y después seleccione **Agente de replicación**.
1. Haga clic en **Crear** para crear el agente.
1. Haga doble clic en el nuevo elemento del agente para que se abra el panel de configuración.
1. Haga clic en **Editar** - se abre el cuadro de diálogo **Configuración del agente** - el **Tipo de serialización** ya está definido como Predeterminado, debe permanecer así.

   * En la ficha **Configuración**:

      * Activar **Habilitado**.
      * Escriba una **descripción**.
      * Establezca **Retraso de reintento** en `60000`.

      * Deje **Tipo de serialización** como `Default`.

   * En la ficha **Transporte**:

      * Introduzca el URI requerido para la nueva instancia de publicación; por ejemplo,

        `https://localhost:4504/bin/receive`.

      * Introduzca la cuenta de usuario específica de la dirección que se utiliza para la replicación.
      * Puede configurar otros parámetros según sea necesario.

1. Haga clic en **OK**.

A continuación, puede probar la operación actualizando y publicando una página en el entorno de Author.

Las actualizaciones aparecen en todas las instancias de publicación que se han configurado como anteriormente.

Si tiene algún problema, puede comprobar los registros en la instancia de autor. Según el nivel de detalle requerido, también puede establecer el **Nivel de registro** en `Debug` mediante el cuadro de diálogo **Configuración del agente**, como se ha indicado anteriormente.

>[!NOTE]
>
>Esto se puede combinar con el uso de [Id. de usuario del agente](#agentuserid) para seleccionar contenido diferente y replicarlo en los entornos de publicación individuales. Para cada entorno de publicación:
>
>1. Configure un agente de replicación para replicar en ese entorno de publicación.
>1. Configure una cuenta de usuario con los derechos de acceso necesarios para leer el contenido replicado en ese entorno de publicación específico.
>1. Asigne la cuenta de usuario como **Id. de usuario del agente** para el agente de replicación.
>

### Configuración de un agente de vaciado de Dispatcher {#configuring-a-dispatcher-flush-agent}

Los agentes predeterminados se incluyen en la instalación. Sin embargo, todavía se necesita una determinada configuración y lo mismo se aplica si está definiendo un nuevo agente:

1. Abra la ficha **Herramientas** en AEM.
1. Haga clic en **Implementación**.
1. Seleccione **Replicación** y luego **Agentes en la publicación**.
1. Haga doble clic en el elemento **Vaciado de Dispatcher** para abrir la descripción general.
1. Haga clic en **Editar** - se abre el cuadro de diálogo **Configuración del agente**:

   * En la ficha **Configuración**:

      * Activar **Habilitado**.
      * Escriba una **descripción**.
      * Deje **Serialization Type** como `Dispatcher Flush` o configúrelo como tal si crea un agente.

      * (opcional) Seleccione **Actualización de alias** para habilitar las solicitudes de invalidación de alias o rutas de vanidad en Dispatcher.

   * En la ficha **Transporte**:

      * Introduzca el URI requerido para la nueva instancia de publicación; por ejemplo,

        `https://localhost:80/dispatcher/invalidate.cache`.

      * Introduzca la cuenta de usuario específica de la dirección que se utiliza para la replicación.
      * Puede configurar otros parámetros según sea necesario.

   Para los agentes de vaciado de Dispatcher, la propiedad URI solo se utiliza si utiliza entradas de host virtual basadas en rutas para diferenciar entre granjas, utilice este campo para dirigirse a la granja para invalidarla. Por ejemplo, la granja n.º 1 tiene un host virtual de `www.mysite.com/path1/*` y la granja n.º 2 lo tiene de `www.mysite.com/path2/*`. Puede usar una dirección URL de `/path1/invalidate.cache` para dirigirse a la primera granja de servidores y `/path2/invalidate.cache` para dirigirse a la segunda.

   >[!NOTE]
   >
   >Si ha instalado AEM en un contexto distinto del contexto predeterminado recomendado, configure los [encabezados HTTP](#extended) en la ficha **Extendido**.

1. Haga clic en **OK**.
1. Vuelva a la ficha **Herramientas**, desde donde puede **Activar** el agente **Vaciado de Dispatcher** (**Agentes en la publicación**).

El agente de replicación **Dispatcher Flush** no está activo en Author. Puede acceder a la misma página en el entorno de publicación utilizando el URI equivalente; por ejemplo, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Control del acceso a los agentes de replicación {#controlling-access-to-replication-agents}

El acceso a las páginas utilizadas para configurar los agentes de replicación se puede controlar mediante permisos de página de usuario o grupo en el nodo `etc/replication`.

>[!NOTE]
>
>La configuración de estos permisos no afecta a los usuarios que replican contenido (por ejemplo, desde la consola Sitios web o la opción de la barra de tareas). El marco de replicación no utiliza la &quot;sesión de usuario&quot; del usuario actual para acceder a los agentes de replicación al replicar páginas.

### Configuración de los agentes de replicación desde CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La creación de agentes de replicación solo se admite en la ubicación del repositorio `/etc/replication`. Esto es necesario para que las ACL asociadas se gestionen correctamente. La creación de un agente de replicación en otra ubicación del árbol puede dar lugar a un acceso no autorizado.

Se pueden configurar varios parámetros de los agentes de replicación mediante CRXDE Lite.

Si se desplaza a `/etc/replication`, podrá ver los tres nodos siguientes:

* `agents.author`
* `agents.publish`
* `treeactivation`

Los dos `agents` contienen información de configuración sobre el entorno apropiado y solo están activos cuando ese entorno se está ejecutando. Por ejemplo, `agents.publish` solo se usa en el entorno de publicación. La siguiente captura de pantalla muestra el agente de publicación en el entorno de creación, como se incluye con AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Supervisión de los agentes de replicación {#monitoring-your-replication-agents}

Para supervisar un agente de replicación:

1. Acceda a la ficha **Herramientas** en AEM.
1. Haga clic en **Replicación**.
1. Haga doble clic en el vínculo a los agentes para el entorno adecuado (el panel izquierdo o el derecho). Por ejemplo, **agentes en Autor**.

   La ventana resultante muestra una descripción general de todos los agentes de replicación para el entorno de creación, incluidos su destino y estado.

1. Haga clic en el nombre del agente apropiado (que es un vínculo) para mostrar información detallada sobre ese agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Aquí puede hacer lo siguiente:

   * Compruebe si el agente está activado.
   * Consulte el objetivo de cualquier replicación.
   * Ver si la cola de replicación está activa (habilitada).
   * Ver si hay algún elemento en la cola.
   * **Actualizar** o **Borrar** para actualizar la visualización de las entradas de la cola. Esto le ayuda a ver que los elementos entran y salen de la cola.

   * **Ver registro** para acceder al registro de cualquier acción por parte del agente de replicación.
   * **Probar conexión** a la instancia de destino.
   * **Forzar reintento** en cualquier elemento en cola, si es necesario.

   >[!CAUTION]
   >
   >No utilice el vínculo &quot;Probar conexión&quot; para la bandeja de salida de replicación inversa en una instancia de publicación.
   >
   >
   >Si se realiza una prueba de replicación para una cola de Bandeja de salida, los elementos anteriores a la replicación de prueba se vuelven a procesar con cada replicación inversa.
   >
   >
   >Si estos elementos existen en cola, se pueden encontrar con la siguiente consulta JCR XPath y deben eliminarse.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replicación por lotes {#batch-replication}

La replicación por lotes no replica páginas o recursos individuales, pero espera a que se active el primer umbral de los dos, según el tiempo o el tamaño.

A continuación, empaqueta todos los elementos de replicación en un paquete, que después se replica como un solo archivo en el publicador.

El publicador desempaqueta todos los elementos, los guarda y vuelve a informar al creador.

### Configuración de replicación por lotes {#configuring-batch-replication}

1. Vaya a `http://serveraddress:serverport/siteadmin`
1. Presione el icono **[!UICONTROL Herramientas]** en la parte superior de la pantalla
1. Desde el carril de navegación del lado izquierdo, vaya a **[!UICONTROL Replicación: agentes en Autor]** y haga doble clic en **[!UICONTROL Agente predeterminado]**.
   * También puede acceder al agente de replicación de publicación predeterminado si va directamente a `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Presione el botón **[!UICONTROL Editar]** situado sobre la cola de replicación.
1. En la siguiente ventana, vaya a la ficha **[!UICONTROL Lote]**:
   ![replicación por lotes](assets/batchreplication.png)
1. Configure el agente.

### Parámetros {#parameters}

* `[!UICONTROL Enable Batch Mode]`: habilita o deshabilita el modo de replicación por lotes
* `[!UICONTROL Max Wait Time]`: tiempo de espera máximo hasta que se inicie una solicitud de lote, en segundos. El valor predeterminado es 2 segundos.
* `[!UICONTROL Trigger Size]`: inicia la replicación por lotes cuando se alcanza este límite de tamaño

## Recursos adicionales {#additional-resources}

Para obtener más información sobre la solución de problemas, lea la página [Solución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md).
