---
title: No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK
description: No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 100%

---

# No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

El problema se aplica a las siguientes versiones:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problema {#issue}

El usuario se encuentra con la siguiente excepción:
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Motivo {#reason}

La excepción se produce cuando ejecuta Experience Manager Forms con Oracle JDK (kit de desarrollo de Java) con una versión superior o igual a las siguientes versiones:

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

Las versiones anteriores y posteriores de Java incluyen nuevos límites de procesamiento XML en la JVM (máquina virtual de Java) que hacen que ciertas operaciones específicas de Forms fallen.

## Solución alternativa {#workaround}

1. Detenga el servidor de Experience Manager Forms.
1. Configure el siguiente argumento JVM para su servidor de aplicaciones:

   `-Djdk.xml.xpathExprOpLimit=2000`

   Establece la propiedad del sistema en JVM en un valor razonablemente alto para que no se alcance el límite predeterminado.

1. Inicie su servidor de Experience Manager Forms.
