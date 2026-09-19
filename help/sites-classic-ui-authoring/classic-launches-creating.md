---
title: Creación de lanzamientos
description: Cree un lanzamiento para poder actualizar las páginas web existentes a la versión nueva que se habilitará más adelante. Al crear un lanzamiento, se especifica un título y la página de origen.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 02fd32c8-7def-45d4-ba3b-d4cb346f5103
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 54%
---
# Creación de lanzamientos{#creating-launches}

Cree un lanzamiento para poder actualizar las páginas web existentes a la versión nueva que se habilitará más adelante. Al crear un lanzamiento, especificará un título y la página de origen:

* El título aparece en **Sidekick**, desde donde los autores pueden acceder para trabajar con él.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede utilizar únicamente la página de origen.
* De forma predeterminada, [Live Copy](/help/sites-administering/msm.md) actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos.

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

## Creación de un lanzamiento {#creating-a-launch}

El siguiente procedimiento crea un lanzamiento.

1. Abra la página de administración del sitio web ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Haga clic en **Nuevo...** y después en **Nuevo lanzamiento...**.
1. En el cuadro de diálogo **Crear lanzamiento**, especifique valores para las siguientes propiedades:

   * **Título del lanzamiento**: el nombre del lanzamiento. El nombre debe ser significativo para los autores.
   * **Página de Source**: La ruta de acceso a la página para la que se va a crear el lanzamiento. De forma predeterminada, se incluyen todas las páginas secundarias.
   * **Excluir páginas secundarias**: seleccione esta opción para crear el lanzamiento solo para la página de origen y no para las páginas secundarias. Esta opción no está seleccionada de forma predeterminada.
   * **Mantener sincronizado**: seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Esto se logra convirtiendo el lanzamiento en [live copy](/help/sites-administering/msm.md).
   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Haga clic en **Crear**.

## Eliminación de un lanzamiento {#deleting-a-launch}

También puede eliminar un lanzamiento.

1. En la [consola de lanzamientos](/help/sites-classic-ui-authoring/classic-launches.md), seleccione el lanzamiento requerido.
1. Haga clic en **Eliminar**; se requiere confirmación:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Al eliminar lanzamientos anidados, primero debe eliminar los niveles inferiores.
