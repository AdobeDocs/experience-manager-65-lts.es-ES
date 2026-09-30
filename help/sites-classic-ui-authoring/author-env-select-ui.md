---
title: Selección de la IU
description: Para mayor comodidad de los usuarios autores, la IU táctil permite cambiar a la IU clásica cuando es necesario.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 781b580a-e4d1-419e-afb1-884c8fb634b9
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%
---
# Selección de la IU{#selecting-your-ui}

Dado que la IU táctil reemplaza a la IU clásica, el usuario o el administrador de la instancia de AEM debe tomar una decisión activa para seguir utilizándola. Dado que la IU clásica ya no se mantiene, no hay forma de que el usuario autor simplemente cambie de la IU clásica a la equivalente en la IU táctil.

Para mayor comodidad de los usuarios autores, la IU táctil permite cambiar a la IU clásica cuando es necesario. Consulte [Selección de la interfaz de usuario](/help/sites-authoring/select-ui.md) en la documentación de creación estándar para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas desde una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambiará automáticamente a la IU táctil, pero puede configurarla con la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **servicio de modo de IU de creación de WCM** (servicio `AuthoringUIMode`). Consulte [Anulaciones de IU para el editor](#uioverridesfortheeditor).

## Configuración de la interfaz de usuario predeterminada para la instancia {#configuring-the-default-ui-for-your-instance}

Un administrador del sistema puede configurar la interfaz de usuario que se ve al iniciar y al iniciar sesión usando [Root Mapping](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Esto se puede sobrescribir por los valores predeterminados de usuario o la configuración de sesión.
