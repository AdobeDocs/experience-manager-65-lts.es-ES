---
title: Preguntas frecuentes
description: Preguntas frecuentes sobre AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 49%

---

# Preguntas frecuentes sobre AEM 6.5 LTS {#faq}

Esta página está diseñada para responder algunas preguntas frecuentes acerca de AEM 6.5 LTS.

## ¿Por qué Adobe ha lanzado 6.5 LTS para AEM?

Adobe sigue profundamente comprometida con la seguridad y estabilidad de las aplicaciones que proporciona. La compatibilidad a largo plazo con AEM 6.5 sienta las bases para futuras actualizaciones de AEM 6.5. En particular, AEM 6.5 LTS incluye compatibilidad con Oracle Java 17 y Java 21, y será la rama de AEM que reciba nuevas funciones e innovaciones de AEM.

## Soy cliente On-Premise, ¿qué sucede si no actualizo a AEM 6.5 LTS?

AEM 6.5 LTS incluye importantes actualizaciones de seguridad y estabilidad, incluida la compatibilidad con Oracle Java 17 y Java 21. Aunque Adobe seguirá admitiendo AEM 6.5 durante al menos los próximos 2 años, se recomienda que las organizaciones empiecen a planificar una actualización a 6.5 LTS.

## ¿Se verán afectadas mis personalizaciones e integraciones existentes si actualizo a AEM 6.5 LTS?

Aunque AEM 6.5 LTS tiene como objetivo mantener la compatibilidad con versiones anteriores, se han eliminado algunas funciones y artefactos heredados.
Es esencial revisar las [notas de la versión](/help/release-notes/release-notes.md#deprecated-and-removed-features) y usar la [herramienta AEM Analyzer](/help/sites-deploying/aem-analyzer.md) para evaluar el impacto en sus personalizaciones e integraciones.

## ¿Cómo puedo garantizar una transición sin problemas a AEM 6.5 LTS?

Para garantizar una transición sin problemas, se recomienda:

* Revisar meticulosamente las [notas de la versión](/help/release-notes/release-notes.md) y la documentación.
* Usar [AEM Analyzer](/help/sites-deploying/aem-analyzer.md) para evaluar la complejidad de la actualización.
* Planear y asignar tiempo y recursos suficientes para el proceso de actualización.
* Participar en las sesiones de habilitación y soporte de Adobe para obtener instrucciones y asistencia.

## ¿Qué son los paquetes de servicio de AEM 6.5 LTS?

Los Service Packs de AEM 6.5 LTS son una actualización acumulativa que incluye todas las correcciones y mejoras realizadas en AEM 6.5 LTS desde su lanzamiento inicial. Se recomienda aplicar el Service Pack más reciente para garantizar que la instancia de AEM esté actualizada con las últimas funciones y parches de seguridad.

## Actualmente estoy en AEM 6.5, ¿puedo actualizar directamente al paquete de servicio AEM 6.5 LTS sin actualizar a la versión AEM 6.5 LTS GA?

Sí, puede actualizar directamente de AEM 6.5 a cualquier paquete de servicio AEM 6.5 LTS. Se recomienda revisar las [notas de la versión](/help/release-notes/release-notes.md) y la sección [Actualización a AEM 6.5 LTS](/help/sites-deploying/upgrade.md).

## Actualmente estoy en AEM 6.5 LTS GA, ¿necesito hacer algún cambio de código para actualizar a AEM 6.5 LTS Service Packs?

No, no es necesario realizar ningún cambio de código para actualizar de AEM 6.5 LTS a AEM 6.5 LTS Service Packs. Sin embargo, siempre se recomienda revisar las [notas de la versión](/help/release-notes/release-notes.md) y probar las personalizaciones e integraciones en un entorno de ensayo antes de aplicar el Service Pack a la instancia de producción.

## Quiero empezar de cero con una nueva configuración de AEM 6.5 LTS, ¿puedo empezar directamente con el paquete de servicio AEM 6.5 LTS?

Sí, puede configurar directamente un nuevo paquete de servicio AEM 6.5 LTS sin configurar la compilación de AEM 6.5 LTS GA. Se recomienda revisar las [notas de la versión](/help/release-notes/release-notes.md) y la sección [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md) para obtener más detalles.
