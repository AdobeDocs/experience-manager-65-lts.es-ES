---
title: No se puede restaurar el repositorio de CRX dañado aplicable al servidor de clúster JEE
description: Conozca los pasos sobre cómo restaurar un repositorio de CRX que esté dañado.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 716d8eb2-2010-4d55-b8fe-bd4f6f256a4d
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%
---
# No se puede restaurar el repositorio de CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms en JEE que utiliza una base de datos relacional, la hora en el equipo que aloja AEM Forms y la base de datos relacional siempre deben estar en sincronización absoluta. Si el tiempo en estos equipos no está sincronizado, es posible que no se pueda acceder al repositorio de CRX de AEM Forms en el servidor JEE. Puede parecer corrupto y volverse inaccesible a través de la URL. Se ha registrado el error `AuthenticationsupportService missing`.

## Requisitos previos {#prerequisites}

Realice la copia de seguridad del repositorio de CRX antes de realizar los pasos mencionados a continuación.

## Solución {#solution}

1. Ir a `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Busque el paquete `oak-core` y compruebe si se está ejecutando.

1. Reinicie el paquete `oak-core` si no se está ejecutando. Si el icono ![Botón de pausa](/help/forms/using/assets/stop.png) está presente frente al paquete `oak-core`, entonces indica que el paquete se encuentra en estado de ejecución.

1. Si el problema sigue sin resolverse, restaure desde el repositorio de CRX desde la copia de seguridad o vuelva a compilar el repositorio de CRX si la copia de seguridad no está disponible.


## Aplicable a {#applies-to}

Esta solución se aplica a AEM Forms en el clúster de JEE.
