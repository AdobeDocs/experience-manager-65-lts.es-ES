---
title: 'Administración de correspondencia: Resolución de problemas'
description: Obtenga información sobre cómo gestionar los errores que surgen durante el proceso de guardar una carta en un entorno de AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '217'
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
