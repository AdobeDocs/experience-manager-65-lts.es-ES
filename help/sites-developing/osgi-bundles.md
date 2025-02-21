---
title: Paquetes OSGi
description: Conozca algunas sugerencias para administrar sus paquetes OSGi en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Paquetes OSGi{#osgi-bundles}

## Uso de versiones semánticas {#use-semantic-versioning}

Se pueden encontrar prácticas recomendadas acordadas para la numeración de versiones semánticas en [https://semver.org/](https://semver.org/).

## No incruste más clases y tarros de los estrictamente necesarios en los paquetes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Las bibliotecas comunes deben dividirse en paquetes independientes. Esto permite reutilizarlos en todos los paquetes. Al envolver un *JAR* en un paquete OSGi, asegúrese de comprobar las fuentes en línea para ver si alguien ya lo ha hecho antes. Algunos lugares comunes para encontrar envoltorios de paquetes existentes son: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Recetas de paquete Eclipse y el Repositorio de paquetes Enterprise de SpringSource.

## Depender de las versiones de paquete más bajas necesarias {#depend-on-the-lowest-needed-bundle-versions}

Para las dependencias en tiempo de compilación en archivos POM, siempre dependen de la versión más baja necesaria que expone la API necesaria. Esto permite una mayor compatibilidad con versiones anteriores y facilita las correcciones de la compatibilidad con versiones anteriores.

## Exportación de un conjunto mínimo de paquetes desde paquetes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Cuando se ha exportado un paquete, se ha creado una API de la que otros pueden depender. Asegúrese de exportar lo menos posible y de que lo que se exporta es una API. Es mucho más fácil tomar un método/clase privado y hacerlo público que tomar algo que se exportó anteriormente y hacerlo privado.

Coloque siempre las implementaciones en un paquete *impl* independiente. De manera predeterminada, *maven-bundle-plugin* exporta cualquier elemento del proyecto que no tenga *impl* en su nombre.

## Siempre defina explícitamente una versión semántica para cada paquete exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Esto permite que los consumidores de su API evolucionen junto con usted. Al hacerlo, siga siempre las prácticas recomendadas de control semántico de versiones. Esto permite a los consumidores de la API saber qué tipos de cambios esperar en una nueva versión.

## Incluir información de tipos de metales donde se expone {#include-metatype-information-where-exposed}

Al especificar información significativa sobre el tipo de metal, facilita la comprensión de sus servicios y componentes en la consola Felix. Puede encontrar una lista de anotaciones y atributos de SCR en: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
