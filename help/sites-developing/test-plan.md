---
title: Compilación del plan de prueba
description: Los casos de prueba individuales se combinan en el plan de prueba
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: b2dfc8fb-7bc4-4b5e-8c8f-1463fdc18e50
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 4%
---
# Compilación del plan de prueba{#compiling-your-test-plan}

Los casos de prueba individuales se fusionarán en el plan de prueba, que también define lo siguiente:

**Prioridades**

Algunas pruebas tendrán más importancia que otras, por lo que es aconsejable indicar su prioridad.

Por ejemplo, ciertas pruebas pueden afectar a una decisión de Go / No-Go y, por lo tanto, deben confirmarse con cada versión intermedia probada.

**Iteraciones**

Si su proyecto utiliza cualquier forma de iteración de desarrollo (que implique la publicación de varias versiones), puede que necesite o desee una indicación de los resultados de cada iteración. Esto puede usarse para indicar:

* qué pruebas se tratarán en qué iteración.
* los resultados observados para las pruebas se repitieron en varias iteraciones.
* que las pruebas prioritarias y las pruebas de las características básicas se repitan a intervalos regulares.

**Probador**

En algún momento puede asignar el equipo de prueba adecuado o una persona de prueba específica (posiblemente en función de la disponibilidad o la experiencia).

**Resumen o descripción general**

Para fines de creación de informes, le recomendamos que proporcione una descripción general de los resultados de las pruebas:

* Porcentaje de pruebas ya cubiertas.
* Porcentaje de éxito/error.
* Cifras específicas relacionadas con las pruebas prioritarias.
