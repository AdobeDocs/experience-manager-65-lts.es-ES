---
title: AEM Forms bloquea las solicitudes HTTP válidas
description: Las comprobaciones de validación XSS de AEM Forms pueden bloquear solicitudes HTTP válidas para clientes que utilizan componentes personalizados. Aprenda a identificar el problema y a relajar temporalmente las comprobaciones de validación.
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 8%
---
# AEM Forms bloquea las solicitudes HTTP válidas {#aem-forms-blocks-valid-http-requests}

## Problema {#issue}

AEM Forms incluye comprobaciones de seguridad para evitar ataques de scripts entre sitios (XSS). Estas comprobaciones pueden bloquear algunas solicitudes HTTP válidas para clientes que utilizan componentes personalizados en AEM Forms. Cuando se bloquea una solicitud, aparece el siguiente mensaje en los registros del servidor:

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>Para una petición POST, el valor predeterminado del parámetro es **1048576**. Para una petición GET, el valor predeterminado del parámetro es **2000**. Para modificar el valor del parámetro para una petición POST, pase el argumento `com.adobe.idp.dsc.provider.rest.httpParamMaxSize` durante el inicio del servidor.

## Causa {#cause}

La regex de validación XSS es más estricta que el formato del valor de parámetro enviado por el componente personalizado, por lo que AEM Forms rechaza la solicitud.

## Resolución {#resolution}

>[!CAUTION]
>
>Al eliminar las comprobaciones de seguridad, el sistema es vulnerable a ataques de scripts entre sitios (XSS). Quite las comprobaciones de seguridad solo como solución temporal.

Para quitar temporalmente las comprobaciones de seguridad y permitir todas las solicitudes HTTP:

1. Detenga el servidor de AEM Forms.

1. Cree una copia de seguridad del archivo `[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear`.

1. Extraiga el archivo `esapi-helper-2.x.x.jar` del archivo `adobe-livecycle-<server_name>.ear`. La ubicación del archivo `esapi-helper-2.x.x.jar` difiere para cada servidor de aplicaciones:

   | Servidor de aplicaciones | Ubicación del archivo esapi-helper-2.x.x.x.jar |
   | --- | --- |
   | JBoss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle WebLogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. Abra los archivos `[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties` y `[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties` para editarlos.

1. Establezca el valor de las siguientes propiedades en `^[\\s\\S]*$`. Por ejemplo, `Validator.HTTPParameterName=^[\\s\\S]*$`. Guarde y cierre los archivos.

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. Empaquetar el `esapi-helper-2.x.x.jar` actualizado en `adobe-livecycle-<application_server_name>.ear`. Implementar el(la) `adobe-livecycle-<application_server_name>.ear` actualizado(a) en el servidor de aplicaciones.

1. Inicie el servidor de AEM Forms.

## Referencia {#references}

* [Mitigación de vulnerabilidades de falsificación de solicitudes del lado del servidor (SSRF) para AEM Forms en JEE 6.5 LTS SP2](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
