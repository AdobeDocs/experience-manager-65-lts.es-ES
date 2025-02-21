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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

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
