---
title: Arquitectura de AEM Forms Workspace
description: Información conceptual y descripción general de la arquitectura de LiveCycle AEM Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 100%

---

# Arquitectura de AEM Forms Workspace {#aem-forms-workspace-architecture}

AEM Forms Workspace es una aplicación web alojada en CRX™. Cuando se abre Workspace en un explorador, se accede a un recurso CRX y la aplicación se representa como una página HTML en el explorador.

La aplicación accede al servidor de AEM Forms en los extremos REST para hacer lo siguiente:

* Buscar tareas de usuario, puntos de inicio de procesos, historial de procesos e información de usuarios
* Realizar acciones en tareas
* Consultar tareas en la base de datos
* Actualizar las preferencias de usuario y mucho más

El servidor de AEM Forms accede a la base de datos de AEM Forms a través de JDBC. La base de datos mantiene las tareas, los procesos y sus instancias, los usuarios y la información relacionada.

AEM Forms Workspace está diseñado en componentes modulares JavaScript™ que pueden personalizarse y reutilizarse de forma individual en otras aplicaciones web. Los componentes se basan en BackBone, que es una biblioteca JavaScript que da estructura a las aplicaciones web. En el siguiente [enlace](/help/forms/using/backbone-interaction.md) encontrará un artículo detallado que describe la interacción de los componentes con BackBone. [Este](/help/forms/using/folder-structure.md) artículo explica la organización de los componentes en la estructura de carpetas CRX.

Paquetes entregados para AEM Forms Workspace:

* `adobe-lc-workspace-pkg-<version>.zip`: es un paquete CRX, es decir, se puede implementar en CRX usando el Administrador de paquetes.
* `adobe-lc-workspace-<version>-src.zip`: es un archivo que contiene el código completo de AEM Forms Workspace y los scripts para crear los paquetes de implementación: los paquetes Ship, Debug y Dev.
