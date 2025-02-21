---
title: Fragmentos de documento
description: Los fragmentos de documento, como texto, listas, condiciones y fragmentos de diseño, de Administración de correspondencia le permiten formar los componentes estáticos, dinámicos y repetibles de la correspondencia del cliente.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 100%

---

# Fragmentos de documento {#document-fragments}

Los fragmentos de documento son partes/componentes reutilizables de una correspondencia mediante los cuales puede componer comunicaciones/cartas interactivas. Los fragmentos del documento son de los siguientes tipos:

* **Texto**: un recurso de texto es un fragmento de contenido que consta de uno o más párrafos de texto. Un párrafo puede ser estático o dinámico.

   * [Textos en comunicaciones interactivas](/help/forms/using/texts-interactive-communications.md)

* **Condición**: las condiciones permiten definir qué contenido se incluye en el momento de la creación de la correspondencia en función de los datos suministrados. La condición se describe en términos de variables de control. Una variable de control puede ser un elemento de diccionario de datos o un marcador de posición.

   * [Condiciones de las comunicaciones interactivas](/help/forms/using/conditions-interactive-communications.md)

* **Lista:** Lista es un grupo de fragmentos de documento, que incluyen texto, listas, condiciones e imágenes. El orden de los elementos de la lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de una lista para replicar un patrón de elementos reutilizable.
* **Fragmento de diseño**: un fragmento de diseño es un diseño que se puede utilizar en una o varias cartas. Un fragmento de diseño se utiliza para crear patrones repetibles, especialmente tablas dinámicas. El diseño puede contener campos de formulario típicos, como “Dirección” y “Número de referencia”. También contiene subformularios vacíos que denotan áreas de destino. Los diseños (XDP) se crean en Designer y luego se cargan en AEM Forms.
