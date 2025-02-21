---
title: Editar lanzamientos
description: Después de crear un lanzamiento para la página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 75%

---

# Edición de lanzamientos{#editing-launches}

## Edición de páginas de lanzamiento {#editing-launch-pages}

Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.

1. Acceda a [Lanzamiento desde las referencias (consola Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Ir a la página** para abrir la página y editarla.

>[!NOTE]
>
>No se le permite mover una página dentro de un lanzamiento. Si se intenta esta acción, se generará un mensaje de advertencia:
>
>* Advertencia: Esta página es el origen de un lanzamiento. No se permite mover la página.

### Editar páginas de lanzamiento sujetas a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Si el lanzamiento se basa en [Live Copy](/help/sites-administering/msm.md), deberá hacer lo siguiente:

* consulte símbolos de bloqueo (pequeños candados) cuando edite un componente (contenido o propiedades).
* consulte la ficha **Live Copy** en **Propiedades de página**

Se utiliza una Live Copy para sincronizar contenido *desde* la rama de origen *a* la rama de lanzamiento (para mantener el lanzamiento actualizado con los cambios realizados en la fuente).

Puede realizar cambios de la misma manera que puede editar una Live Copy estándar; por ejemplo:

* Al hacer clic en un candado cerrado, se interrumpe esta sincronización y se le permite realizar nuevas actualizaciones del contenido en el lanzamiento. Una vez desbloqueados (candado abierto), los cambios no se sobrescribirán con ningún cambio realizado en la misma ubicación dentro de la rama de origen.
* **Suspender** (y **reanudar**) la herencia de una página específica.

Consulte [Cambio del contenido de Live Copy](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para obtener más información.

## Comparación de una página de lanzamiento con su página de origen {#comparing-a-launch-page-to-its-source-page}

Para rastrear los cambios realizados, puede ver el lanzamiento en **Referencias** y comparar la página de lanzamiento con la página de origen:

1. En la consola **Sites**, [vaya a la página de origen del lanzamiento y selecciónela](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. Abra el panel **[Referencias](/help/sites-authoring/basic-handling.md#references)** y seleccione **Lanzamientos**.
1. Seleccione el lanzamiento específico y luego **Comparar con el origen**:

   ![captura de pantalla_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. Las dos páginas (inicio y origen) se abrirán una junto a la otra.

   Para obtener información completa sobre el uso de esta funcionalidad, consulte [Diferencias de página](/help/sites-authoring/page-diff.md).

## Cambio de las páginas de origen utilizadas {#changing-the-source-pages-used}

Puede añadir en cualquier momento las páginas en el rango de páginas de origen para el lanzamiento, o eliminarlas: 

1. Acceda y seleccione el lanzamiento de:

   * la [consola Lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

      * Seleccione **Editar**.

   * [Referencias (consola Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles:

      * Seleccione **Editar lanzamiento**. 

   Se muestran las páginas de origen.

1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

   >[!NOTE]
   >
   >Para añadir páginas a un lanzamiento, deben estar debajo de una raíz de idioma común; es decir, dentro de un solo sitio.

## Edición de una configuración de lanzamiento {#editing-a-launch-configuration}

Las propiedades del lanzamiento se pueden editar en cualquier momento:

1. Acceda y seleccione el lanzamiento de:

   * la [consola Lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

      * Seleccione **Propiedades**.

   * [Referencias (consola Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles:

      * Seleccione **Editar propiedades**. 

   Se muestran los detalles.

1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

   Consulte [Lanzamientos: el orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener información sobre el propósito y la interacción de los campos **Fecha de lanzamiento** y **Listo para producción**.

## Descubrimiento del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

El estado se muestra al seleccionar un lanzamiento específico en la pestaña Referencias (consulte [Lanzamientos en referencias (consola Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console)).

![captura de pantalla_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
