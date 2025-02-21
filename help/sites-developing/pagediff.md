---
title: Desarrollo y diferencia de página
description: Aprenda a desarrollar y utilizar la función de diferencia de página en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# Desarrollo y diferencia de página{#developing-and-page-diff}

## Descripción general de funciones {#feature-overview}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar la versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar la página actual con una versión anterior en paralelo con las diferencias resaltadas.

La diferencia de página permite al usuario comparar la página actual con lanzamientos, versiones anteriores, etc. Para obtener detalles sobre esta característica de usuario, consulte [Diferencias de página](/help/sites-authoring/page-diff.md).

## Detalles de operación {#operation-details}

Al comparar versiones de una página, la versión anterior que el usuario desea comparar se vuelve a crear en AEM en segundo plano para facilitar la comparación. Esto es necesario para poder procesar el contenido [para una comparación en paralelo](/help/sites-developing/pagediff.md#operation-details).

Esta operación de recreación la realiza AEM de forma interna, es transparente para el usuario y no requiere intervención. Sin embargo, un administrador que visualice el repositorio, por ejemplo, en CRXDE Lite, vería estas versiones recreadas dentro de la estructura de contenido.

Cuando se compara contenido, todo el árbol hasta la página para comparar se vuelve a crear en la siguiente ubicación:

`/tmp/versionhistory/`

Se ejecuta automáticamente una tarea de limpieza para limpiar este contenido temporal.

## Permisos {#permissions}

Anteriormente, en la IU clásica, se debía tener en cuenta un desarrollo especial para facilitar la diferenciación de AEM (como usar la biblioteca de etiquetas `cq:text` o la integración personalizada del servicio OSGi `DiffService` en los componentes). Esto ya no es necesario para la nueva función de diferencia, ya que la diferencia se produce en el lado del cliente mediante la comparación DOM.

Sin embargo, hay algunas limitaciones que el desarrollador debe tener en cuenta.

* Esta función utiliza clases CSS que no están separadas por espacios de nombres al producto de AEM. Si se incluyen en la página otras clases CSS personalizadas o clases CSS de terceros con los mismos nombres, la visualización de la diferencia puede verse afectada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Dado que la comparación de diferencias es del lado del cliente y se ejecuta al cargar la página, no se contabilizará ningún ajuste en el DOM después de ejecutar el servicio de comparación de diferencias del lado del cliente. Esto puede afectar a

   * Componentes que utilizan AJAX para incluir contenido
   * Aplicaciones de una sola página
   * Componentes basados en JavaScript que manipulan el DOM tras la interacción del usuario.

>[!NOTE]
>
>La comparación de diferencias de página solo funciona para los componentes que tienen nodos cq:editConfig válidos.
