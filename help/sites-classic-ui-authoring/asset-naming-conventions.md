---
title: Convenciones de nomenclatura para pruebas de recursos
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del repositorio de contenido Java. Sin embargo, Adobe Experience Manager impone más convenciones para el nombre de los nodos de recursos.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 37de1a8b-b7db-469e-98a7-20ddb6218510
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 9%
---
# Convenciones de nomenclatura para pruebas de recursos{#naming-conventions-for-assets-testing}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura de [Repositorio de contenido Java](/help/sites-developing/the-basics.md#java-content-repository). Sin embargo, Adobe Experience Manager impone más convenciones para el nombre de los nodos de recursos.

## IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre del recurso cuando un nombre de nodo explícito:

  * se proporciona un título de recurso para la conversión en el nombre del nodo
  * se proporciona un nombre de nodo explícito

* Caracteres válidos (solo estos caracteres son realmente válidos cuando se crea un recurso desde la IU clásica):

  * &#39;a&#39; a &#39;z&#39;
  * De &#39;A&#39; a &#39;Z&#39;
  * De &#39;0&#39; a &#39;9&#39;
  * _ (guion bajo)
  * `-` (guión/signo menos)
