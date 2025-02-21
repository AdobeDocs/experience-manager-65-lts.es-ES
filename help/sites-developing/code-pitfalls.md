---
title: Peligros de código
description: Problemas comunes de codificación que se deben evitar al desarrollar para AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Peligros de código{#code-pitfalls}

## Evite los enlaces de Sling en el código Java {#avoid-sling-bindings-in-java-code}

Los enlaces de Sling son una forma inadecuada de obtener acceso a un servicio en el 90 % de los casos. En su lugar, debe usar *@Reference* o *@Inject* anotaciones.

## Evite Thread.interrupt en el código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* es peligroso porque puede cerrar archivos, incluidos los archivos Lucene y los archivos de caché persistente, cuando se llama en el momento incorrecto.

## Evite mezclar la sincronización de Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Esto puede provocar una condición de carrera en la que el código se interbloqueará finalmente.
