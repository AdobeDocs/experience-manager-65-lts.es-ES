---
title: 'Administración de correspondencia: Resolución de problemas'
description: Obtenga información sobre cómo gestionar los errores que surgen durante el proceso de guardar una carta en un entorno de AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 57794b13-471b-4aae-aa57-ddfc2dfc58c9
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 83%
---
# Administración de correspondencia: Resolución de problemas {#correspondence-management-troubleshooting}

## Errores al guardar una carta {#errors-when-saving-a-letter}

### Problema {#issue}

Se muestra uno de los siguientes errores al guardar una carta:

* El enlace de datos no está presente para el módulo de texto.
* Proporcione la información de la propiedad necesaria para lo siguiente

### Motivo {#reason}

Estos errores pueden producirse debido a uno de los siguientes factores:

* Un diccionario de datos está enlazado a la carta pero no está presente en el servidor.
* Un diccionario de datos está enlazado a la carta, pero incluye un guion bajo (_) en su nombre.

### Solución alternativa {#workaround}

Asegúrese de que el diccionario de datos que utiliza en la carta esté presente en el servidor y que no incluya guiones bajos (_) en su nombre.

## Error al previsualizar una carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Al previsualizar una carta, aparece el error “Error al cargar la carta: no se pudo importar el recurso desde la entrada XML” incluso cuando se publica un recurso de texto que n no se ha publicado previamente en la carta.

### Solución alternativa {#workaround-1}

Restablezca la memoria caché de la carta en la instancia de publicación mediante los siguientes pasos y vuelva a intentar visualizar la carta:

1. Vaya a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e inicie sesión como administrador.
1. Seleccione **Configuraciones de Administración de correspondencia**.
1. En **Configuraciones de Administración de correspondencia**, deshabilite **Habilitar memoria caché de la carta** y haga clic en **Guardar**.
1. Marque **Habilitar memoria caché de la carta** y haga clic en **Guardar**.
1. Vuelva a intentar visualizar la carta.
