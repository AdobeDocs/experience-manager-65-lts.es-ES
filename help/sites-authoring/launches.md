---
title: Uso de lanzamientos para desarrollar contenido para una versión futura
description: Launch le permite desarrollar contenido de forma eficaz para una versión futura. Permiten realizar cambios listos para su publicación futura, manteniendo al mismo tiempo las páginas actuales.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 77%

---

# Lanzamientos{#launches}

Los lanzamientos le permiten desarrollar contenido con eficacia para una versión futura.

Se crea un lanzamiento para permitirle realizar cambios listos para su publicación futura (sin perder de vista las páginas actuales). Después de editar y actualizar las páginas de lanzamiento, estas se vuelven a promocionar al origen y luego se activan las páginas de origen (nivel superior). La promoción duplica el contenido del lanzamiento en las páginas de origen y se puede realizar de forma manual o automática (según los campos establecidos a la hora de crear y editar el lanzamiento).

Por ejemplo, las páginas de productos de temporada de su tienda en línea se actualizan trimestralmente para que los productos destacados se correspondan con la temporada actual. Para preparar la próxima actualización trimestral, se puede crear un lanzamiento de las páginas web correspondientes. Durante el trimestre, se acumulan los cambios siguientes en la copia de lanzamiento:

* Cambios en las páginas de origen que se producen como resultado de tareas normales de mantenimiento. Estos cambios se duplican automáticamente en las páginas de lanzamiento.
* Ediciones que se realizan en las páginas de lanzamiento directamente en preparación para el trimestre siguiente.

Cuando llegue el trimestre siguiente, las páginas de lanzamiento se promocionan de forma que se puedan publicar las páginas de origen (que contienen el contenido actualizado). Puede promocionar todas las páginas o solamente aquellas que se han modificado. 

También se puede realizar lo siguiente:

* Se han creado lanzamientos para varias ramas de raíz. Si bien puede crear el lanzamiento para todo el sitio (y realizar los cambios allí), este método es poco práctico, ya que es necesario copiar todo el sitio. Cuando hay cientos o incluso miles de páginas implicadas, los requisitos del sistema y el rendimiento se ven afectados por la acción de copiar y, posteriormente, por las comparaciones necesarias para las tareas de promoción.
* Cree lanzamientos anidados (un lanzamiento dentro de otro lanzamiento). Esto permite crear un lanzamiento a partir de uno existente, de modo que los autores puedan aprovechar los cambios ya realizados, en lugar de tener que realizar los mismos cambios varias veces para cada lanzamiento.

En esta sección se describe cómo crear, editar y promocionar (y, si es necesario, [eliminar](/help/sites-authoring/launches-creating.md#deleting-a-launch)) páginas de lanzamiento desde la consola Sitios o [la consola Lanzamientos](#the-launches-console):

* [Creación de lanzamientos](/help/sites-authoring/launches-creating.md)
* [Edición de lanzamientos](/help/sites-authoring/launches-editing.md)
* [Promoción de lanzamientos](/help/sites-authoring/launches-promoting.md)

## Lanzamientos: orden de eventos {#launches-the-order-of-events}

Los lanzamientos permiten desarrollar contenido con eficacia para una versión futura de una o más páginas web activadas.

Los lanzamientos le permiten:

* Cree una copia de las páginas de origen:

   * La copia es su lanzamiento.
   * Las páginas de origen de nivel superior se denominan **Producción**.

      * Las páginas de origen puedan obtenerse de varias ramas (separadas).

  ![Información general sobre las acciones de inicio](assets/chlimage_1-111.png)

* Edite la configuración de lanzamiento:

   * Adición o eliminación de páginas o ramas en el lanzamiento.
   * Editar propiedades de lanzamiento; como **Título**, **Fecha de lanzamiento** e indicador **Listo para la producción**.

* Es posible promocionar y publicar el contenido de forma manual o automática:

   * Manualmente:

      * Promocione de nuevo el contenido del lanzamiento en el **Destino** (páginas de origen) cuando esté listo para su publicación.
      * Publique el contenido de las páginas de origen (tras volver a promocionarlo).
      * Promocione todas las páginas o solo las páginas modificadas.

   * Automáticamente. Esto implica lo siguiente:

      * El campo **Fecha**(**Live**) **de lanzamiento**: esto se puede establecer al crear o editar un lanzamiento. 

      * El indicador **Producción lista**: esto solo se puede establecer al editar un lanzamiento.
      * Si se establece el indicador **Listo para la producción**, el lanzamiento se promocionará automáticamente a las páginas de producción en el **Lanzamiento**(**Activo**) **fecha** especificado. Después de la promoción, las páginas de producción se publican automáticamente.\
        Si no se ha establecido ninguna fecha, el indicador no tiene ningún efecto.

* Actualice las páginas de origen y de lanzamiento en paralelo:

   * Los cambios que se realicen en las páginas de origen se implementan automáticamente en la copia de lanzamiento (si está configurada con herencia; es decir, como Live Copy). 
   * Los cambios en la copia de lanzamiento se pueden realizar sin interrumpir las actualizaciones automáticas o las páginas de origen. 

  ![Información general sobre actualizaciones](assets/chlimage_1-112.png)

* [Crear un lanzamiento anidado](/help/sites-authoring/launches-creating.md#creating-a-nested-launch): un lanzamiento dentro de un lanzamiento:

   * El origen es un lanzamiento existente.
   * Puede [promocionar un lanzamiento anidado](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch) a cualquier destino; puede ser un lanzamiento principal o las páginas de origen de nivel superior (producción).

  ![Información general sobre el lanzamiento anidado](assets/chlimage_1-113.png)

  >[!CAUTION]
  >
  >Al eliminar un lanzamiento, se quitarán el lanzamiento en sí y todos los lanzamientos anidados descendentes.

>[!NOTE]
>
>La creación y edición de lanzamientos requieren derechos de acceso a `/content/launches`, como con el grupo predeterminado `content-authors`.
>
>Si experimenta algún problema, póngase en contacto con el administrador del sistema. 

>[!CAUTION]
>
>No se admite la reordenación de componentes en una página de Launch.
>
>Cuando se promocione la página, se reflejarán los cambios de contenido, pero las posiciones de los componentes no cambiarán.

## La consola Lanzamientos {#the-launches-console}

La consola Lanzamientos proporciona una descripción general de los lanzamientos y le permite realizar acciones con los enumerados. Se puede acceder a la consola desde: 

* La consola **Herramientas**: **Herramientas**, **Sitios** **Lanzamientos**.

* O directamente con [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## Lanzamientos en referencias (consola Sites) {#launches-in-references-sites-console}

1. En la consola **Sites**, vaya al origen de los lanzamientos.
1. Abra el carril **Referencias** y seleccione la página de origen.
1. Seleccione **Lanzamientos**, se enumerarán los lanzamientos existentes:

   ![Pestaña Referencia: lanzamientos](assets/screen-shot_2019-03-05at121901-1.png)

1. Haga clic en el lanzamiento adecuado. Se mostrará una lista de acciones posibles:

   ![Seleccionar lanzamiento para mostrar posibles acciones](assets/screen-shot_2019-03-05at121952-1.png)
