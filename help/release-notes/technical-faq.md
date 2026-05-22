---
title: Preguntas técnicas frecuentes (FAQ)
description: Preguntas técnicas frecuentes sobre AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f994a8712a403083de1edc62579846ba99bd3afd
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 59%

---

# Preguntas técnicas frecuentes sobre AEM 6.5 LTS {#technical-faq}

Esta página está diseñada para responder algunas preguntas técnicas frecuentes acerca de AEM 6.5 LTS.

## Preguntas técnicas frecuentes

### El punto final `/systemalive` ya no está disponible en AEM 6.5 LTS.

El paquete Felix System Ready configurado para proporcionar el punto final `/systemalive` ha quedado obsoleto y ha sido reemplazado por Apache Felix Health Checks. Este paquete ya no se incluye en AEM 6.5 LTS.

El nuevo punto final de comprobación de estado está disponible en `/system/health` y se implementa mediante Apache Felix Health Checks.

Para obtener documentación detallada sobre el marco de trabajo Felix Health Check, consulte la [documentación de felix](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md).

### Compatibilidad con AEM Groovy Console

La versión de la consola Groovy de AEM que se estaba usando en AEM 6.5 podría no funcionar en AEM 6.5 LTS debido a la falta de dependencias de guayaba. La versión recién admitida de la consola Groovy de AEM es [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip).

#### Se requiere una configuración adicional para la consola de AEM Groovy

Si utiliza la consola Groovy de AEM, debe agregar explícitamente la siguiente configuración OSGi para `com.adobe.granite.apicontroller.FilterResolverHookFactory`. Agregue `aem-groovy-console-bundle` a la lista de paquetes permitidos para la clave `org.apache.sling.distribution.api`, ampliando los valores predeterminados de plataforma:

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### ¿Admite AEM 6.5 LTS la sincronización de usuarios?

Sí, AEM 6.5 LTS admite la sincronización de usuarios. No hay cambios en la funcionalidad de sincronización de usuarios entre AEM 6.5 y 6.5 LTS.

### Uber JAR en Maven Central parece estar dañado, ¿cuál es el problema?

Verifique que está utilizando Uber JAR con el clasificador `apis`. Tenga en cuenta que la estructura de empaquetado de Uber JAR ha cambiado en AEM 6.5 LTS. Para obtener más información, consulte [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### ¿AEM 6.5 LTS es compatible con los espacios de nombres del paquete `jakarta.*` (por ejemplo, `jakarta.annotation`)?

No. AEM 6.5 LTS no admite artefactos de Sling migrados a los espacios de nombres del paquete `jakarta.*`. Use los equivalentes de `javax.*` en su código y dependencias; por ejemplo, `javax.annotation.PostConstruct` en lugar de `jakarta.annotation.PostConstruct` en los modelos Sling. La implementación de modelos Sling en AEM 6.5 LTS solo reconoce las anotaciones `javax.*`, por lo que las anotaciones `jakarta.*` se omiten silenciosamente durante la inicialización.

Para obtener más información, consulte el artículo de la base de conocimiento [Los modelos Sling con `jakarta.annotation.PostConstruct` producen un error en AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-30339).

## Obtención de ayuda adicional

Si tiene problemas que no se tratan aquí:
* Revise las [notas de la versión](/help/release-notes/release-notes.md) para ver si hay problemas conocidos.
* Póngase en contacto con el servicio de asistencia de Adobe para obtener ayuda.
