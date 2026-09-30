---
title: Dificultades en el código
description: Problemas comunes de codificación que se deben evitar al desarrollar para AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 95656312-2648-455e-80fb-3e03bf1cd633
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 4%
---
# Dificultades en el código{#code-pitfalls}

## Evite los enlaces de Sling en el código Java {#avoid-sling-bindings-in-java-code}

Los enlaces de Sling son una forma inadecuada de obtener acceso a un servicio en el 90 % de los casos. En su lugar, debe usar *@Reference* o *@Inject* anotaciones.

## Evite Thread.interrupt en el código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* es peligroso porque puede cerrar archivos, incluidos los archivos Lucene y los archivos de caché persistente, cuando se llama en el momento incorrecto.

## Evite mezclar la sincronización de Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Esto puede provocar una condición de carrera en la que el código se interbloqueará finalmente.
