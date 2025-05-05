---
title: Solución de problemas de integración
description: Obtenga información sobre cómo solucionar problemas al integrarse con Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---

# Solución de problemas de integración{#troubleshooting-integration-issues}

## Sugerencias generales de resolución de problemas {#general-troubleshooting-tips}

### Asegúrese de que no haya errores de JavaScript {#ensure-there-are-no-javascript-errors}

Compruebe si la consola JavaScript del explorador muestra algún error. Los errores no controlados pueden impedir que el código siguiente se ejecute correctamente. En caso de errores, compruebe qué secuencia de comandos está causando el error y en qué área. La ruta al script puede dar una indicación de a qué funcionalidad pertenece el script.

### Inicio de sesión en el nivel de componente {#logging-on-component-level}

En algunos casos, podría resultar útil añadir instrucciones adicionales en el nivel de componente. Dado que el componente se procesa, puede agregar un marcado temporal para mostrar valores de variables que puedan ayudarle a identificar posibles problemas. Por ejemplo:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Para obtener más información acerca del registro, vea las páginas [Registro](/help/sites-deploying/configure-logging.md) y [Trabajo con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Problemas de integración de Analytics {#analytics-integration-issues}

### El importador de informes causa un uso elevado de la memoria/CPU {#the-report-importer-causes-high-cpu-memory-usage}

El importador de informes causa un uso elevado de CPU/Memoria o `OutOfMemoryError` excepciones.

#### Solución {#solution}

Para solucionar este problema, puede probar lo siguiente:

* Asegúrese de que no haya una gran cantidad de importadores de encuestas registrados (consulte la sección &quot;El cierre tarda mucho tiempo debido al importador de encuestas&quot; más abajo).
* Ejecute importadores de informes a una hora determinada del día mediante expresiones CRON para las configuraciones `ManagedPollingImporter` en la [consola OSGi](/help/sites-deploying/configuring-osgi.md).

Para obtener más información acerca de la creación de servicios de importador de datos personalizados en AEM, lea el siguiente artículo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### El cierre tarda mucho tiempo debido al importador de encuestas {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics se ha diseñado teniendo en cuenta un mecanismo de herencia. Normalmente, habilita Analytics para un sitio al agregar una referencia a una configuración de Analytics en la pestaña de propiedades de página [Cloud Services](/help/sites-developing/extending-cloud-config.md). A continuación, la configuración se hereda automáticamente a todas las páginas secundarias sin necesidad de volver a hacer referencia a ella a menos que una página requiera una configuración diferente. Al agregar una referencia a un sitio, también se crean automáticamente varios nodos (12 para AEM 6.3 y versiones anteriores o 6 para AEM 6.4   y posterior) del tipo `cq;PollConfig` que crea una instancia de los importadores de encuestas utilizados para importar datos de Analytics en AEM. Como resultado:

* Tener muchas páginas que hacen referencia a Analytics lleva a una gran cantidad de importadores de encuestas.
* Además, copiar y pegar páginas con una referencia a una configuración de Analytics provoca una duplicación de los importadores de encuestas.

#### Solución {#solution-1}

En primer lugar, analizar [error.log](/help/sites-deploying/configure-logging.md) puede ofrecerle alguna perspectiva sobre la cantidad de importadores de encuestas activos o registrados. Por ejemplo:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

En segundo lugar, asegúrese de que solo las páginas principales (las que están en la parte superior de la jerarquía) tengan una configuración de Analytics a la que se haga referencia.

Para obtener más información acerca de la creación de servicios de importador de datos personalizados en AEM, lea el siguiente artículo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas de DTM (heredados) {#dtm-legacy-issues}

### La etiqueta de script de DTM no se representa en el origen de página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

La etiqueta de script [DTM](/help/sites-administering/dtm.md) no se incluye correctamente en la página a pesar de que se hace referencia a la configuración en la pestaña de propiedades de página [Cloud Services](/help/sites-developing/extending-cloud-config.md).

#### Solución {#solution-2}

Para solucionar el problema, puede probar lo siguiente:

* Asegúrese de que las propiedades cifradas se puedan descifrar (tenga en cuenta que el cifrado puede utilizar una clave generada automáticamente diferente en cada instancia de AEM). Para obtener más información, lea [Compatibilidad con cifrado para propiedades de configuración](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Volver a publicar las configuraciones encontradas en `/etc/cloudservices/dynamictagmanagement`
* Compruebe las ACL en `/etc/cloudservices`. Las ACL deben ser:

   * permitir; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/defaults/`&ast;
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/defaults`
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/public/`&ast;
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/public`

Para obtener más información sobre la administración de ACL, lea la página [Administración de usuarios y seguridad](/help/sites-administering/security.md#permissions-in-aem).

## Problemas de integración de Target {#target-integration-issues}

### Contenido dirigido no visible en el modo de vista previa al utilizar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Este problema se debe a que los componentes de página personalizados no incluyen las bibliotecas de cliente o JSP correctas que administran las integraciones de Target DTM.

#### Solución {#solution-3}

Puede probar las siguientes soluciones:

* Asegúrese de que el elemento personalizado `headlibs.jsp` (si existe `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) incluya lo siguiente:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Asegúrese de que el `head.html` personalizado (si corresponde a `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **no** incluya de forma selectiva encabezados de integración específicos como el ejemplo siguiente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

`servicelibs.jsp` agrega los objetos JavaScript de análisis necesarios y carga las bibliotecas del servicio en la nube asociadas al sitio web. Para el servicio de Target, las bibliotecas se cargan mediante `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

El conjunto de bibliotecas que se cargan depende del tipo de biblioteca de cliente de destino ( `mbox.js` o `at.js`) utilizada en la configuración de Target.

Cuando use DTM para entregar `mbox.js` o `at.js`, asegúrese de que las bibliotecas se carguen antes de que se represente el contenido. El uso de sistemas Tag Management que carguen estas bibliotecas de forma asíncrona podría causar problemas al ejecutar el código de JavaScript específico de destinatario.

Para obtener más información, lea la página [Desarrollo de contenido de destino](/help/sites-developing/target.md#understanding-the-target-component).

### El error &quot;Falta la ID del grupo de informes en la inicialización de AppMeasurement&quot; se muestra en la consola del explorador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Este problema puede aparecer cuando Adobe Analytics se implementa en el sitio web mediante DTM y utiliza código personalizado. La causa está usando `s = new AppMeasurement()` para crear una instancia del objeto `s`.

#### Solución {#solution-4}

Utilice `s_gi` en lugar del método de instanciación `new AppMeasurement`. Por ejemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Se muestra aleatoriamente una oferta predeterminada en lugar de la oferta correcta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Este problema puede tener varias causas:

* La carga asincrónica de bibliotecas de cliente de Target (`mbox.js` o `at.js`) mediante sistemas Tag Management de terceros puede interrumpir el direccionamiento de forma aleatoria. Se supone que las bibliotecas de Target se cargan sincrónicamente en el encabezado de la página. Esto siempre ocurre cuando las bibliotecas se envían desde AEM.

* Cargando dos bibliotecas de cliente de Target (`at.js`) simultáneamente, por ejemplo, una que usa DTM y otra que usa la configuración de Target en AEM. Esto puede provocar conflictos en la definición de `adobe.target` si las versiones de `at.js` difieren.

#### Solución {#solution-5}

Puede probar las siguientes soluciones:

* Asegúrese de que el código de cliente que carga las bibliotecas similares a la DTM (que a su vez cargan las bibliotecas de Target) se ejecute sincrónicamente en [encabezado de página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* si el sitio está configurado para usar DTM con el fin de ofrecer bibliotecas de Target, asegúrese de que la opción **Clientlib deliverby DTM** esté marcada en la [configuración de Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) para el sitio.

### Siempre se muestra una oferta predeterminada en lugar de la oferta correcta al utilizar AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

AEM 6.2 y 6.3 no es compatible con la versión 1.3.0 o posterior de AT.js. Con la versión 1.3.0 de AT.js que introduce la validación de parámetros para sus API, `adobe.target.applyOffer()` requiere un parámetro &quot;mbox&quot; que no proporciona el código `atjs-itegration.js`.

#### Solución {#solution-6}

Para resolver este problema, edite `atjs-itegration.js` y agregue el campo `"mbox": mboxName` en el objeto de parámetro de `adobe.target.applyOffer()` de la siguiente manera:

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### La página Objetivos y configuración no muestra la sección Fuentes de informes {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Es muy probable que este problema sea un problema de aprovisionamiento de [A4T Analytics Cloud Configuration](/help/sites-administering/target-configuring.md).

#### Solución {#solution-7}

Debe comprobar que A4T está correctamente habilitado para su cuenta de Target mediante la emisión de la siguiente solicitud de verificación a AEM:

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Si la respuesta contiene la línea `a4tEnabled:false`, póngase en contacto con el [Servicio de atención al cliente de Adobe](https://helpx.adobe.com/contact.html) para que su cuenta se aprovisione correctamente.

### API de Target útiles {#helpful-target-apis}

A continuación se presentan dos API de Target que pueden resultar útiles para solucionar problemas de Target:

* Recuperar el extremo de Target para un código de cliente determinado

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperación del perfil de un cliente

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
