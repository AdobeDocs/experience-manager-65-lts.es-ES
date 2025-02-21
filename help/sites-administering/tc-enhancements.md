---
title: Mejoras de traducción
description: Mejoras y refinamientos incrementales de las funciones de administración de traducciones de AEM.
topic-tags: site-features
content-type: reference
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 26%

---

# Mejoras de traducción{#translation-enhancements}

Esta página presenta mejoras y ampliaciones progresivas de las funciones de administración de traducciones de AEM.

## Automatización del proyecto de traducción {#translation-project-automation}

Se han añadido opciones para mejorar la productividad al trabajar con proyectos de traducción, como promocionar y eliminar automáticamente los lanzamientos de traducción y programar la ejecución recurrente de un proyecto de traducción.

1. En el proyecto de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **Resumen de traducción**.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la ficha **Avanzado**. En la parte inferior, puede seleccionar **Promocionar automáticamente los lanzamientos de traducción**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. De forma opcional, puede seleccionar si, después de recibir contenido traducido, los lanzamientos de traducción deben promocionarse y eliminarse automáticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para seleccionar la ejecución recurrente de un proyecto de traducción, seleccione la frecuencia con el menú desplegable en **Repetir traducción**. La ejecución recurrente de proyectos creará y ejecutará automáticamente trabajos de traducción en los intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Proyectos de traducción multilingües {#multilingual-translation-projects}

Es posible configurar varios idiomas de destino en un proyecto de traducción para reducir el número total de proyectos de traducción creados.

1. En el proyecto de traducción, haga clic en los puntos de la parte inferior del mosaico **Resumen de traducción**.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la ficha **Avanzado**. Puede agregar varios idiomas en **Idioma de destino**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Alternativamente, si está iniciando la traducción a través del carril de referencias en Sites, agregue sus idiomas y seleccione **Crear proyecto de traducción en varios idiomas**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Se crearán trabajos de traducción en el proyecto para cada idioma de destino. Se pueden iniciar uno a uno dentro del proyecto o todos a la vez ejecutando el proyecto globalmente en Administración de proyectos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Actualizaciones de memoria de traducción {#translation-memory-updates}

Las ediciones manuales del contenido traducido se pueden sincronizar de nuevo con el sistema de gestión de traducciones (TMS) para mejorar su memoria de traducción.

1. Desde la consola Sites, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria de traducción**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista de lista muestra una comparación en paralelo de la fuente y la traducción de cada componente de texto editado. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y **Actualizar memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM actualiza la traducción de las cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.

* La acción actualiza la traducción de cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.
* No crea nuevos trabajos de traducción.
* Envía las traducciones de vuelta al sistema de administración de etiquetas, a través de la API de traducción de AEM (se muestra a continuación).

Para usar esta función, haga lo siguiente:

* Configure un sistema de administración de etiquetas para su uso con AEM.
* El conector debe implementar el método [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * El código dentro de este método determina qué sucede con la solicitud de actualización de memoria de traducción.
   * El marco de traducción de AEM envía los pares de valor de cadena (traducción original y actualizada) al sistema de gestión de etiquetas mediante esta implementación de método.

Las actualizaciones de la memoria de traducción se pueden interceptar y enviar a un destino personalizado, en los casos en que se utilice una memoria de traducción propia.

## Copias de idioma en varios niveles {#language-copies-on-multiple-levels}

Las raíces de los idiomas ahora se pueden agrupar en nodos, por ejemplo, por región, aunque se siguen reconociendo como raíces de las copias de idiomas.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Solo se permite un nivel. Por ejemplo, lo siguiente no permitirá que la página &quot;es&quot; resuelva una copia de idioma:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>No se detectará esta copia de idioma `es` porque está a 2 niveles (américa/centroamérica) del nodo `en`.

>[!NOTE]
>
>Las raíces de idioma pueden tener cualquier nombre de página, en lugar de solo el código ISO del idioma. AEM comprobará siempre primero la ruta y el nombre, pero si el nombre de la página no identifica un idioma, AEM comprobará la propiedad cq:language de la página para identificar el idioma.

## Informes de estado de traducción {#translation-status-reporting}

Ahora se puede seleccionar una propiedad en la vista de lista de sitios que muestre si una página se ha traducido, está en proceso de traducción o aún no se ha traducido. Para mostrarlo:

1. En Sitios, cambie a **Vista de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Haga clic en **Ver configuración**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Marque la casilla **Traducido** en **Traducción** y haga clic en **Actualizar**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ahora puede ver una columna **Traducido** que muestra el estado de traducción de las páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
