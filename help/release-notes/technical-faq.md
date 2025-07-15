---
title: Preguntas más frecuentes técnicas (FAQ)
description: Preguntas técnicas frecuentes sobre AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: ec722773ce3acff1d0de861523db8ff7df552c4b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# Preguntas frecuentes técnicas sobre AEM 6.5 LTS {#technical-faq}

Esta página está diseñada para responder algunas preguntas técnicas frecuentes acerca de AEM 6.5 LTS.

## Preguntas frecuentes técnicas

### El extremo `/systemalive` ya no está disponible en AEM 6.5 LTS.

El paquete Felix System Ready configurado para proporcionar el extremo `/systemalive` ha quedado obsoleto y ha sido reemplazado por las comprobaciones de estado de Apache Felix. Este paquete ya no se incluye en AEM 6.5 LTS.

El nuevo extremo de comprobación de estado está disponible en `/system/health` y se implementa mediante las comprobaciones de estado de Apache Felix.

Para obtener documentación detallada sobre el marco de la comprobación de estado de Felix, consulte la [documentación de Felix](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md).

### Compatibilidad con la consola Groovy de AEM

La versión de la consola de AEM Groovy que se estaba usando en AEM 6.5 podría no funcionar en AEM 6.5 LTS debido a la falta de dependencias de guayaba. La nueva versión compatible de la consola Groovy de AEM es [19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8).

### ¿AEM 6.5 LTS admite la sincronización de usuarios?

Sí, AEM 6.5 LTS admite la sincronización de usuarios. No hay cambios en la funcionalidad de sincronización de usuarios entre AEM 6.5 y 6.5 LTS.

### El JAR de Uber en Maven Central parece estar corrupto — ¿cuál es el problema?

Compruebe que está utilizando Uber JAR con el clasificador `apis`. Tenga en cuenta que la estructura de empaquetado del JAR de Uber ha cambiado en AEM 6.5 LTS. Para obtener más información, consulte [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

## Obtención de ayuda adicional

Si tiene problemas que no se tratan aquí:
* Revise las [notas de la versión](/help/release-notes/release-notes.md) para ver si hay problemas conocidos.
* Póngase en contacto con el servicio de asistencia de Adobe para obtener ayuda.
