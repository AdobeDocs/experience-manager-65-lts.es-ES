---
title: Mitigación de vulnerabilidades de falsificación de solicitudes del lado del servidor (SSRF) para AEM Forms en JEE 6.5 LTS SP2
description: Pasos de mitigación para vulnerabilidades de falsificación de solicitudes del lado del servidor (SSRF) en implementaciones de AEM Forms en JEE 6.5 LTS Service Pack 2 que se ejecutan en JBoss.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1d825cd821609504c5e2cff7f7002bf3afe30434
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%

---

# Mitigación de vulnerabilidades de falsificación de solicitudes del lado del servidor (SSRF) para AEM Forms en JEE 6.5 LTS SP2

## Referencia rápida {#quick-reference}

| Nivel de impacto | Versiones afectadas | Acción recomendada |
| --- | --- | --- |
| Crítico | AEM Forms en el paquete de servicio 2 de JEE 6.5 LTS (6.5 LTS SP2) | Instalar manualmente [revisión](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| No afectado | AEM Forms en OSGi, Workbench, Cloud Service | No se requiere ninguna acción |

**Vulnerabilidades resueltas:**

* Falsificación de solicitudes del lado del servidor (SSRF) (CWE-918)

## Información general {#overview}

### Qué se ve afectado {#whats-affected}

| Vulnerabilidad | Impacto | Componentes afectados |
| --- | --- | --- |
| Falsificación de solicitudes del lado del servidor (SSRF) (CWE-918) | Los atacantes pueden inducir al servidor a realizar solicitudes no deseadas a recursos internos o externos | AEM Forms en JEE 6.5 LTS SP2 |

### Qué no se ve afectado {#whats-not-affected}

* Experience Manager Forms Workbench (todas las versiones)
* Experience Manager Forms en OSGi (todas las versiones)
* Experience Manager Forms as a Cloud Service

## Opciones de resolución {#resolution-options}

### Antes de comenzar {#before-you-start}

Antes de realizar cualquier cambio, realice una copia de seguridad del archivo EAR que está a punto de reemplazar:

* Busque `adobe-edcserver-jboss.ear` en el directorio de implementación:

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* Copie el archivo en una ubicación de copia de seguridad segura fuera del directorio de implementación.
* Asegúrese de que la copia de seguridad esté completa y accesible antes de continuar con cualquier actualización.

Esta precaución le permite restaurar el estado original en caso de que encuentre algún problema durante el proceso de actualización.

### Instalación manual de revisión para AEM Forms en JEE 6.5 LTS SP2 (JBoss)

1. Descargar `adobe-edcserver-jboss.ear` del [Portal de distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear).

1. Busque `adobe-edcserver-jboss.ear` en el directorio de implementación y reemplácelo por el archivo descargado:

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. Inicie el Administrador de configuración de AEM Forms para volver a implementar el EAR actualizado y aplicar la revisión.

1. Reinicie el servidor de aplicaciones y confirme la implementación correcta desde los registros del servidor.

## Referencia {#references}

* [Prácticas recomendadas de seguridad de Adobe Experience Manager Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
