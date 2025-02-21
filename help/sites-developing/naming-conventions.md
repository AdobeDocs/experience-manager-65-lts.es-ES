---
title: Convenciones de nomenclatura de nodos en el repositorio de contenido Java
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del repositorio de contenido de Java
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Convenciones de nomenclatura {#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura de [Repositorio de contenido Java](/help/sites-developing/the-basics.md#java-content-repository). Sin embargo, AEM impone más convenciones para el nombre de los nodos de página.

## Convenciones de nomenclatura para páginas {#naming-conventions-for-pages}

Estas convenciones de nomenclatura se implementan en varios niveles:

* JcrUtil: la implementación de AEM de [las utilidades JCR](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) proporciona métodos para operaciones a nivel de página.
* Según la interfaz de usuario utilizada:

   * [IU estándar con capacidad táctil](#standard-ui)
   * [IU clásica](#classic-ui)

### Utilidades JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) es la implementación de AEM de las utilidades JCR. De especial interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`

   * Comprueba si el nombre no está vacío y contiene solo caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.

* `createValidName`

   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) proporciona métodos para operaciones a nivel de página, basados en [JCRUtil](#jcr-utilities).

### IU estándar {#standard-ui}

La interfaz de usuario táctil estándar:

* Valida el nombre según las restricciones impuestas por PageManager cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

### IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre cuando un nombre de nodo explícito cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

* Caracteres válidos (en realidad, solo estos caracteres son válidos cuando se crea una página desde la interfaz de usuario clásica, aunque `PageManagerImpl` permitiría caracteres adicionales):

   * &#39;a&#39; a &#39;z&#39;
   * De &#39;A&#39; a &#39;Z&#39;
   * De &#39;0&#39; a &#39;9&#39;
   * _ (guion bajo)
   * `-` (guión/signo menos)
