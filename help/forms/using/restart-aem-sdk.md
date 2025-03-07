---
title: ¿Cómo reiniciar el SDK de AEM?
description: Prácticas recomendadas para reiniciar el SDK de AEM
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: 68935045-89b1-4219-b111-88a4600200df
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 100%

---

# Reinicio del SDK de AEM

Si reinicia el SDK de AEM deteniendo los procesos de Java™, puede dar lugar a incoherencias en el entorno de desarrollo de AEM y producirse un error como:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Solución

Para reiniciar el SDK de AEM, vaya a la ventana de comandos activa y pulse el comando `Ctrl + C` para reiniciar el SDK.

Se recomienda utilizar el comando “Ctrl + C” para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java™, puede generar incoherencias en el entorno de desarrollo de AEM.
