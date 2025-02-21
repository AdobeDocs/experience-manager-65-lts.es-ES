---
title: Editor
description: Aprenda a volver al Editor de IU clásico.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Editor{#editor}

De forma predeterminada, se ha deshabilitado la capacidad para cambiar a la IU clásica desde el editor.

Para volver a habilitar la opción **Abrir en la IU clásica** en el menú **Información de la página**, siga estos pasos.

1. Con CRXDE Lite, busque el siguiente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Por ejemplo

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Cree una superposición con la opción **Nodo de superposición**; por ejemplo:

   * **Ruta**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Ubicación de superposición**: `/apps/`
   * **Tipos de nodos coincidentes**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad de texto de varios valores al nodo superpuesto:

   `sling:hideProperties = ["granite:hidden"]`

1. La opción **Abrir en la IU clásica** vuelve a estar disponible en el menú **Información de la página** al editar páginas.

   ![abrir en la opción de IU clásica a partir de la información de página](assets/syui-03-2019-02-27-15-19-48.png)
