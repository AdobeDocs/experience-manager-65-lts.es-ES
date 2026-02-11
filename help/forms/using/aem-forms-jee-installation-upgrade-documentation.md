---
title: Flujo de trabajo de instalación y actualización para AEM Forms en JEE
description: Flujo de trabajo de instalación y actualización para AEM Forms 6.5 LTS en JEE (JBoss), con una lista consolidada de PDF relevantes y su propósito.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# Flujo de trabajo de instalación y actualización para AEM Forms en JEE {#aem-forms-jee-installation-upgrade-documentation}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Utilice el siguiente flujo de trabajo y tablas para elegir las guías correctas para su escenario. Algunos documentos se publican como PDF; con el tiempo, se pueden añadir documentos adicionales a medida que están disponibles.

## Flujo de trabajo de instalación y actualización {#installation-upgrade-workflow}

1. Revise [Plataformas compatibles con AEM Forms en JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) y asegúrese de que su sistema cumple las combinaciones de software y hardware requeridas.
2. Decide si estás realizando una **instalación nueva** o una **actualización**.
3. Para la ruta elegida, siga la secuencia descrita a continuación (algunos escenarios requieren más de una guía).

## Pasos previos a la instalación y a la actualización {#start-here}

| Guía | Descripción |
| --- | --- |
| [Plataformas compatibles con AEM Forms en JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) | Enumera las combinaciones de software y hardware compatibles con AEM Forms en JEE. Use esto para validar los requisitos previos antes de iniciar una instalación o actualización. |
| [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) | Explica las arquitecturas recomendadas y las topologías de implementación para que pueda elegir un enfoque que coincida con su entorno (por ejemplo, un solo servidor o clúster). |
| [Elegir un tipo de persistencia para una instalación de AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | Ayuda a seleccionar un tipo de persistencia adecuado para la topología de instalación antes de comenzar. |

## ¿Cómo instalo Adobe Experience Manager Forms (AEM Forms) en JEE en JBoss? {#installing-aem-forms-jee-jboss}

### Llave en mano {#install-jee-jboss-turnkey}

| Guía | Descripción |
| --- | --- |
| [Instalación e implementación de AEM Forms 6.5 LTS en JEE mediante JBoss Turnkey (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | Use para una **instalación llave en mano** nueva en JBoss. Este documento proporciona instrucciones para instalar e implementar AEM Forms en JEE mediante la distribución llave en mano de JBoss. |

### Servidor único (no llave en mano) {#install-jee-jboss-single-server}

| Guía | Descripción |
| --- | --- |
| [Preparando la instalación de AEM Forms (un solo servidor) (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | Use **antes** de una **instalación nueva de un solo servidor (que no sea llave en mano)**. Este documento enumera los requisitos previos y los pasos de preparación del entorno para instalar AEM Forms en JEE en una topología de un solo servidor. |
| [Instalación e implementación de AEM Forms en JEE para JBoss (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | Use para la **instalación e implementación paso a paso** de AEM Forms en JEE en JBoss (**sin llave en mano**). Para instalaciones de un solo servidor, siga esta guía **después de que** complete *Preparación para instalar AEM Forms (un solo servidor)*. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## ¿Cómo actualizo Adobe Experience Manager Forms (AEM Forms) en JEE en JBoss? {#upgrading-aem-forms-jee-jboss}

### Llave en mano {#upgrade-jee-jboss-turnkey}

| Guía | Descripción |
| --- | --- |
| [Actualización a AEM Forms 6.5 LTS en JEE para JBoss Turnkey (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | Use para una **actualización completa**. Este documento proporciona instrucciones para actualizar un AEM Forms existente en la instalación llave en mano de JEE JBoss. |

### Servidor único {#upgrade-jee-jboss-single-server}

| Guía | Descripción |
| --- | --- |
| [Preparándose para actualizar AEM Forms (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | Use **antes** de **actualizar un solo servidor**. Describe cómo preparar el entorno antes de actualizar a AEM 6.5 LTS Forms. Se aplica a entornos que ejecutan AEM Forms en JEE en un modo de instalación de un solo servidor. |
| [Actualización a AEM Forms en JEE para JBoss (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | Use para el **procedimiento de actualización paso a paso** en JBoss en un modo de instalación de **un solo servidor**. Siga esta guía **después de que** complete *Preparación para actualizar AEM Forms*. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

