---
title: Mitigación de las vulnerabilidades de VULN-36128 y VULN-36120 para AEM Forms en JEE 6.5 LTS SP2
description: Pasos de mitigación para VULN-36128 y VULN-36120 en implementaciones de AEM Forms en JEE 6.5 LTS Service Pack 2 que se ejecutan en JBoss.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1b876f20cbc3a00a02a4449f0d353fb858695235
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---

# Mitigación de las vulnerabilidades de VULN-36128 y VULN-36120 para AEM Forms en JEE 6.5 LTS SP2

## Referencia rápida {#quick-reference}

| Nivel de impacto | Versiones afectadas | Acción recomendada |
| --- | --- | --- |
| Crítico | AEM Forms en el paquete de servicio 2 de JEE 6.5 LTS (6.5 LTS SP2) | Instalar manualmente [revisión](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| No afectado | AEM Forms en OSGi, Workbench, Cloud Service | No se requiere ninguna acción |

**Vulnerabilidades resueltas:**

* **VULN-36128**: vulnerabilidad de ejecución de código remoto que permite que atacantes remotos no autorizados ejecuten código arbitrario.
* **VULN-36120**: vulnerabilidad de validación de entrada incorrecta que podría permitir el acceso no autorizado a información confidencial.

## Pasos de mitigación {#mitigation-steps}

### Antes de comenzar {#before-you-start}

Antes de realizar cualquier cambio, haga una copia de seguridad del archivo EAR que va a reemplazar:

* Busque `adobe-edcserver-jboss.ear` en el directorio de implementación:

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* Copie el archivo en una ubicación de copia de seguridad segura fuera del directorio de implementación.
* Asegúrese de que la copia de seguridad esté completa y accesible antes de continuar con cualquier actualización.

Esta precaución le permite restaurar el estado original si se produce algún problema durante el proceso de actualización.

### Instalación manual de revisión para AEM Forms en JEE 6.5 LTS SP2 (JBoss) {#manual-hotfix-installation-aem-forms-jee-65-lts-sp2-jboss}

1. Descargar `adobe-edcserver-jboss.ear` del [Portal de distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear).

1. Busque `adobe-edcserver-jboss.ear` en el directorio de implementación y reemplácelo por el archivo descargado:

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. Inicie el Administrador de configuración de AEM Forms para volver a implementar el EAR actualizado y aplicar completamente el parche.

1. Reinicie el servidor de aplicaciones y confirme la implementación correcta desde los registros del servidor.

## Referencias {#references}

* [Prácticas recomendadas de seguridad de Adobe Experience Manager Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
