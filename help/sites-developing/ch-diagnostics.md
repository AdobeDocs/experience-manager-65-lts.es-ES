---
title: Diagnóstico de ContextHub
description: ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de trabajo de ContextHub
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Diagnóstico de ContextHub {#contexthub-diagnostics}

ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de trabajo de ContextHub. Para abrir la página, vaya a la página `contexthub.diagnostics.html` de la instancia de autor de AEM, por ejemplo:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

La página Diagnósticos de ContextHub proporciona información sobre los almacenes y los módulos de interfaz de usuario que se han creado, las carpetas de la biblioteca de cliente que se cargan y los vínculos a páginas útiles.

>[!NOTE]
>
>Para que se devuelva la información de diagnóstico, debe habilitarse el modo de depuración; de lo contrario, la página de diagnósticos estará en blanco. Consulte [este documento](ch-configuring.md#debugging-contexthub) para obtener detalles sobre cómo habilitar el modo de depuración.

>[!NOTE]
>
>Para las configuraciones de ContextHub que aún se encuentran en sus rutas heredadas, la ubicación de la página de diagnóstico es `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Tiendas {#stores}

La sección Tiendas enumera todas las tiendas de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **Título:** El [tipo de almacén](/help/sites-developing/ch-samplestores.md) en el que se basa el almacén.
* **ruta de acceso:** Ruta de acceso al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta de acceso del nodo del repositorio donde se define el tipo de almacén.
* **clientlibs:** Las categorías de las bibliotecas de cliente cargadas que implementan el tipo de almacén.

## Módulos {#modules}

La sección Módulos enumera todos los módulos de interfaz de usuario de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **Título:** [Tipo de módulo de interfaz de usuario](/help/sites-developing/ch-samplemodules.md) en el que se basa el módulo de interfaz de usuario.
* **ruta de acceso:** Ruta de acceso al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta de acceso del nodo del repositorio donde se define el tipo de módulo de interfaz de usuario.
* **clientlibs:** Las categorías de las bibliotecas de cliente cargadas que implementan el tipo de módulo de interfaz de usuario.

## Clientlibs {#clientlibs}

La sección Clientlibs enumera todas las carpetas de la biblioteca de cliente que ContextHub ha cargado. Las bibliotecas de cliente se clasifican en:

* **kernel.js:** Bibliotecas de cliente que implementan el marco de trabajo de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** bibliotecas de cliente que implementan los tipos de módulos de interfaz de usuario e interfaz de usuario de ContextHub.
* **style.css:** archivos CSS cargados desde bibliotecas de cliente.

## URL {#urls}

La sección Direcciones URL contiene vínculos a funciones de ContextHub:

* **Editor de configuración:** Abre la [página Configuración de ContextHub](ch-configuring.md), donde puede configurar tiendas, modos de interfaz de usuario y módulos de interfaz de usuario.

* **Configuración de los módulos de ContextHub:** Abre el archivo /etc/cloudsettings/default/contexthub.config.kernel.js, que contiene la representación de objeto de JavaScript de las configuraciones de almacén de ContextHub.
* **Configuración de la interfaz de usuario de ContextHub:** Abre el archivo /etc/cloudsettings/default/contexthub.config.ui.js, que contiene la representación de objeto de JavaScript de las configuraciones del modo de interfaz de usuario de ContextHub.
* **kernel.js:** Abre el archivo /etc/cloudsettings/default/contexthub.kernel.js, que contiene el código fuente de las bibliotecas de cliente que implementan el marco de trabajo de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** Abre el archivo /etc/cloudsettings/default/contexthub.ui.js, que contiene el código fuente de las bibliotecas de cliente que implementan los tipos de módulos de IU e IU de ContextHub.
* **style.css:** Abre el archivo /etc/cloudsettings/default/contexthub.styles.css, que contiene los estilos CSS para los módulos de IU e IU de ContextHub.
