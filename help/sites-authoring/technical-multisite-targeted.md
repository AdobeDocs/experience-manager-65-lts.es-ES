---
title: Estructurar la administración de diversos sitios para el contenido segmentado
description: Un diagrama muestra cómo se estructura la compatibilidad con varios sitios para el contenido de destino
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 36%

---

# Estructurar la administración de diversos sitios para el contenido segmentado{#how-multisite-management-for-targeted-content-is-structured}

El diagrama siguiente muestra cómo se estructura la compatibilidad con varios sitios para el contenido de destino.

Las áreas aparecen debajo de **/content/campaigns/&lt;brand>** y, de forma predeterminada, cada marca tiene un área principal, que se crea automáticamente. Cada área tiene su propio conjunto de actividades, experiencias y ofertas.

![chlimage_1-268](assets/chlimage_1-268.png)

Para buscar contenido de destino, las páginas o sitios pueden asignarse a un área. Si no hay ningún área configurada, AEM vuelve al área principal para esta marca específica.

En el diagrama siguiente se muestra un ejemplo de cómo funciona la lógica para tres sitios, llamados site1, site2 y site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 busca myarea1 para brand1 y otherarea2 para brand2 en función de la asignación de áreas.
* site2 busca myarea1 para brand1 y área principal para brand2, ya que solo se define la asignación de área para brand1.
* site3 busca el área principal para brand1 y brand2, ya que no se ha definido ninguna otra asignación de área para este sitio.
