---
title: Desarrollo de proxy [!DNL Assets]
description: 'Un proxy es una instancia de  [!DNL Experience Manager]  que usa trabajadores proxy para procesar trabajos. Obtenga información sobre cómo configurar un proxy, operaciones admitidas, componentes proxy y cómo desarrollar un trabajador proxy personalizado. [!DNL Experience Manager] '
contentOwner: AG
role: Admin, Architect
solution: Experience Manager, Experience Manager Assets
feature: Proxy Workers
exl-id: 8de16e9d-40b6-49d2-9e6b-1aba13137d78
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Desarrollo de proxy [!DNL Assets] {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utiliza un proxy para distribuir el procesamiento de ciertas tareas.

Un proxy es una instancia de Experience Manager específica (y a veces independiente) que utiliza los trabajadores proxy como procesadores responsables de gestionar un trabajo y crear un resultado. Un trabajador proxy puede utilizarse para una amplia variedad de tareas. Si hay un proxy [!DNL Assets], se puede usar para cargar recursos para procesar en Assets. Por ejemplo, el [trabajador de proxy IDS](indesign.md) usa un servidor [!DNL Adobe InDesign] para procesar archivos y usarlos en Assets.

Cuando el proxy es una instancia de [!DNL Experience Manager] independiente, esto ayuda a reducir la carga en las instancias de creación de [!DNL Experience Manager]. De manera predeterminada, [!DNL Assets] ejecuta las tareas de procesamiento de recursos en la misma JVM (externalizada mediante proxy) para reducir la carga en la instancia de creación de [!DNL Experience Manager].

## Proxy (acceso HTTP) {#proxy-http-access}

Hay un proxy disponible a través del servlet HTTP cuando está configurado para aceptar trabajos de procesamiento en: `/libs/dam/cloud/proxy`. Este servlet crea un trabajo de sling a partir de los parámetros registrados. A continuación, se agrega a la cola de trabajos del proxy y se conecta al trabajador del proxy correspondiente.

### Operaciones admitidas {#supported-operations}

* `job`

  **Requisitos**: el parámetro `jobevent` debe establecerse como un mapa de valor serializado. Se usa para crear un `Event` para un procesador de trabajos.

  **Resultado**: Agrega un nuevo trabajo. Si se realiza correctamente, se devuelve un ID de trabajo único.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **Requisitos**: se debe establecer el parámetro `jobid`.

  **Resultado**: devuelve una representación JSON del nodo de resultado creado por el procesador de trabajos.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

  **Requisitos**: se debe establecer el parámetro jobid.

  **Resultado**: Devuelve un recurso asociado con el trabajo dado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

  **Requisitos**: se debe establecer el parámetro jobid.

  **Resultados**: quita un trabajo si se encuentra.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Trabajador Proxy {#proxy-worker}

Un trabajador proxy es un procesador responsable de gestionar un trabajo y crear un resultado. Los trabajadores residen en la instancia de proxy y deben implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para que se reconozca como trabajador de proxy.

>[!NOTE]
>
>El trabajador debe implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para que se reconozca como trabajador proxy.

### API de cliente {#client-api}

[`JobService`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html) está disponible como servicio OSGi que proporciona métodos para crear trabajos, quitar trabajos y obtener resultados de esos trabajos. La implementación predeterminada de este servicio (`JobServiceImpl`) utiliza el cliente HTTP para comunicarse con el servlet proxy remoto.

A continuación se muestra un ejemplo de uso de API:

```java
@Reference
 JobService proxyJobService;

 // to create a job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Configuraciones de Cloud Service {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Las configuraciones de trabajo de proxy y proxy están disponibles mediante configuraciones de servicios en la nube a las que se puede acceder desde la consola [!DNL Assets] **Herramientas** o en `/etc/cloudservices/proxy`. Se espera que cada trabajador proxy agregue un nodo bajo `/etc/cloudservices/proxy` para los detalles de configuración específicos del trabajador (por ejemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte [Configuración de InDesign Server Proxy Worker](indesign.md#configuring-the-proxy-worker-for-indesign-server) y [Configuración de Cloud Services](../sites-developing/extending-cloud-config.md) para obtener más información.

A continuación se muestra un ejemplo de uso de API:

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Desarrollo de un trabajador proxy personalizado {#developing-a-customized-proxy-worker}

El [trabajador de proxy IDS](indesign.md) es un ejemplo de un trabajador de proxy [!DNL Assets] que ya se proporciona de forma predeterminada para externalizar el procesamiento de recursos de InDesign.

También puede desarrollar y configurar su propio trabajador proxy [!DNL Assets] para crear un trabajador especializado que distribuya y subcontrate sus tareas de procesamiento [!DNL Assets].

La configuración de su propio trabajador de proxy personalizado requiere lo siguiente:

* Configurar e implementar (con eventos de Sling):

   * un tema de trabajo personalizado
   * un controlador de eventos de trabajo personalizado

* A continuación, utilice la API de JobService para:

   * enviar el trabajo personalizado al proxy
   * administre su trabajo

* Si desea utilizar el proxy de un flujo de trabajo, debe implementar un paso externo personalizado mediante la API WorkflowExternalProcess y la API JobService.

El siguiente diagrama y pasos detallan cómo proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>En los pasos siguientes, se indican los equivalentes de InDesign como ejemplos de referencia.

1. Se ha usado un [trabajo de Sling](https://sling.apache.org/site/eventing-and-jobs.html), por lo que debe definir un tema de trabajo para su caso de uso.

   Por ejemplo, vea `IDSJob.IDS_EXTENDSCRIPT_JOB` para el trabajador del proxy IDS.

1. El paso externo se utiliza para almacenar en déclencheur el evento y luego esperar hasta que termine; esto se hace sondeando el ID. Desarrolle su propio paso para implementar nuevas funciones.

   Implemente un `WorkflowExternalProcess` y, a continuación, utilice la API de JobService y el tema del trabajo para preparar un evento de trabajo y enviarlo al JobService (un servicio OSGi).

   Por ejemplo, consulte `INDDMediaExtractProcess`.java para el trabajador del proxy IDS.

1. Implemente un controlador de trabajo para el tema. Este controlador requiere desarrollo para que realice la acción específica y se considere la implementación de trabajador.

   Por ejemplo, vea `IDSJobProcessor.java` para el trabajador del proxy IDS.

1. Use `ProxyUtil.java` en dam-commons. Esto permite enviar trabajos a los trabajadores mediante el proxy DAM.

>[!NOTE]
>
>Lo que el marco proxy [!DNL Assets] no proporciona de forma predeterminada es el mecanismo del grupo.
>
>La integración de [!DNL InDesign] permite el acceso a un grupo de [!DNL InDesign] servidores (IDSPool). Este conjunto es específico de la integración de [!DNL InDesign] y no forma parte del marco del proxy [!DNL Assets].

>[!NOTE]
>
>Sincronización de resultados:
>
>Con n instancias que utilizan el mismo proxy, el resultado del procesamiento permanece con el proxy. Es tarea del cliente (Autor de Experience Manager) solicitar el resultado utilizando el mismo ID de trabajo único que se le proporcionó al cliente al crear el trabajo. El proxy simplemente realiza el trabajo y mantiene el resultado listo para solicitarlo.
