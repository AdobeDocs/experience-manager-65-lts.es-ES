---
product: adobe experience manager
description: Documentación de Adobe Experience Manager 6.5 LTS.
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.en
index: true
type: Documentation
solution: Experience Manager, Experience Manager 6.5 LTS
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
  - id: ae206583-dab1-444b-b978-a37aad4a988c
usetq: true
landing-page-name: experience-manager-lts
landing-page-breadcrumb-title: AEM 6.5 LTS
version: Experience Manager 6.5 LTS
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 934301c6c517f5dddc438ee6bc06a8fbcf3d036b
workflow-type: tm+mt
source-wordcount: 93
ht-degree: 2%

---


# Metadatos para uso interno

Los metadatos del sistema de creación de GitHub son jerárquicos y se definen con los siguientes niveles crecientes de precedentes.

1. metadata.md
1. ToC
1. Artículo

Los metadatos definidos en el archivo metadata.md se aplican a todo el repositorio, pero se pueden sobrescribir en los niveles de TDC y de artículo. Cualquier anulación de los metadatos debe realizarse en el nivel más bajo posible.

Los metadatos del repositorio experience-manager-cloud-service.en son los mínimos requeridos.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

Artículo

* `title`
* `description`
* `contentOwner` (solo en contenido de recursos principales bajo `/help/assets`)
