---
title: Aplicación de flujos de trabajo a páginas
description: Los flujos de trabajo se pueden iniciar desde la consola Sitios web o, al editar una página, desde Sidekick.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 15%

---

# Aplicación de flujos de trabajo a páginas{#applying-workflows-to-pages}

A la hora de aplicar el flujo de trabajo, se especifica la siguiente información:

* Flujo de trabajo que se va a aplicar.

  Puede aplicar cualquier flujo de trabajo (al que tenga acceso, según lo haya asignado el administrador de AEM).
* Opcionalmente:

   * Un comentario que proporciona información sobre por qué ha iniciado el flujo de trabajo.
   * Título que ayuda a identificar la instancia de flujo de trabajo en la bandeja de entrada de un usuario.

>[!NOTE]
>
>Los administradores de AEM pueden iniciar flujos de trabajo utilizando [otros métodos](/help/sites-administering/workflows-starting.md).

## Aplicación de flujos de trabajo {#applying-workflows}

Los flujos de trabajo se pueden iniciar desde la consola Sitios web o, al editar una página, desde Sidekick.

La columna **Estado** de la consola **Sitios web** indica si se ha aplicado un flujo de trabajo a una página:

![estado del flujo de trabajo](assets/workflowstatus.png)

### Inicio de un flujo de trabajo desde la consola Sitios web {#starting-a-workflow-from-the-websites-console}

1. Abra la consola Sitios web. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. En el árbol Sitios web, seleccione el elemento principal de la página a la que desea aplicar el flujo de trabajo.
1. En la lista de la página, seleccione la página y haga clic en Flujo de trabajo.
1. En el cuadro de diálogo Iniciar flujo de trabajo, seleccione el flujo de trabajo que desea aplicar. Opcionalmente, introduzca un comentario y un título. A continuación, haga clic en Start.

### Iniciar un flujo de trabajo con Sidekick {#starting-a-workflow-using-sidekick}

1. Abra la consola Sitios web.
1. Abra la página requerida.
1. Seleccione la pestaña Flujo de trabajo de Sidekick.
1. Expanda el cuadro de diálogo **Flujo de trabajo**, lo que le permite seleccionar **Flujo de trabajo** y, opcionalmente, escribir **Título del flujo de trabajo** y **Comentario**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. Haga clic en **Iniciar flujo de trabajo** para iniciar una nueva instancia de flujo de trabajo con las propiedades que configuró y la página actual como carga útil. Ahora el flujo de trabajo se está ejecutando.
