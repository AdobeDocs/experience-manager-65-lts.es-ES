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
