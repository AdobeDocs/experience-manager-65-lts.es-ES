---
title: Creación y administración de ofertas
description: Utilice la consola Ofertas para crear ofertas que se pueden usar en las experiencias de actividad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 73%

---

# Creación y administración de ofertas{#creating-and-managing-offers}

Utilice la consola Ofertas para crear ofertas que se puedan [usar en las experiencias de actividad](/help/sites-authoring/content-targeting-touch.md). La creación de ofertas en la consola Ofertas ahorra tiempo cuando varias experiencias requieren la misma oferta:

* Cree una oferta una vez en la biblioteca y utilícela en varias experiencias de las actividades de marca.
* Cambie la oferta en la biblioteca y el cambio afectará a todas las experiencias que la utilicen.

La consola Ofertas organiza las ofertas por marca. Cada marca contiene una biblioteca de ofertas que se pueden utilizar en las experiencias de una marca. Utilice carpetas para definir una estructura jerárquica y organizar las ofertas en cada biblioteca. Una estructura lógica de carpetas permite a los autores encontrar fácilmente ofertas mediante la exploración. Las herramientas de etiquetado y búsqueda también permiten a los autores encontrar ofertas.

## Adición de una marca mediante la consola Ofertas {#add-a-brand-using-the-offers-console}

Cree una marca con la que se asocien sus ofertas. Abra una marca en la consola de ofertas para acceder a la biblioteca de ofertas, donde podrá crear carpetas y ofertas.

Cuando crea una marca mediante la consola Ofertas, también aparece en la [Consola Actividades](/help/sites-authoring/activitylib.md) donde puede añadir y administrar actividades para la marca.

1. En la consola de navegación, haga clic en **Personalization** > **Ofertas**.

   ![screen-shot_2019-03-05at124139-1](assets/screen-shot_2019-03-05at124139-1.png)

1. Haz clic en **Crear** y luego en **Crear** **Marca**.
1. Seleccione la plantilla de marca y haga clic en **Siguiente**.
1. Escriba un título para la marca tal como desea que aparezca en las consolas Ofertas y Actividades. De forma opcional, escriba o seleccione una o varias etiquetas para asociarlas a la marca.
1. Haga clic en **Crear**.

## Añadir una carpeta a una biblioteca de ofertas {#add-a-folder-to-an-offer-library}

Añada una carpeta a la biblioteca de ofertas de una marca para organizar y almacenar las ofertas. Puede crear una carpeta debajo de la marca o de otras carpetas.

1. En la consola Ofertas, abra la ubicación en la que desea crear la carpeta. Por ejemplo, abra la marca para crear una carpeta de nivel superior o abra otra carpeta de la biblioteca.
1. Haga clic en **Crear** > **Crear carpeta u oferta**.

   ![captura de pantalla_2019-03-05at124557](assets/screen-shot_2019-03-05at124557.png)

1. Seleccione **Carpeta** y haga clic en **Siguiente**.
1. Escriba un título para la carpeta tal y como desea que aparezca en la biblioteca de ofertas y escriba o seleccione las etiquetas.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Haga clic en **Crear**.

## Adición de una oferta a una biblioteca de ofertas {#add-an-offer-to-an-offer-library}

Añada una oferta a la biblioteca de ofertas de una marca para que se pueda añadir a las experiencias de la marca. Al añadir una oferta, es necesario escribir un título. También puede asociar la oferta con una o más etiquetas para mejorar la capacidad de búsqueda.

Después de crear la oferta, puede abrirla para crear el contenido.

1. En la consola Ofertas, abra la ubicación donde desea crear la oferta. Por ejemplo, abra la marca para crear una oferta de nivel superior o abra una carpeta en la biblioteca.
1. Haga clic en **Crear** > **Crear carpeta u oferta**.

   ![screen-shot_2019-03-05at124557-1](assets/screen-shot_2019-03-05at124557-1.png)

1. Seleccione la plantilla **Página de ofertas** y haga clic en **Siguiente**.
1. Escriba un título para la oferta y, opcionalmente, seleccione o escriba una o más etiquetas para asociarlas a la oferta. A continuación, haga clic en **Crear**.
1. En el cuadro de diálogo de confirmación, para abrir la oferta y editarla, haga clic en **Abrir página**.

## Edición de una oferta {#editing-an-offer}

Abra una oferta y edite el contenido tal como desea que aparezca en las experiencias que la utilizan. Cuando edita una oferta que se utiliza en cualquier experiencia, los cambios aparecen en las experiencias.

Puede abrir una oferta desde una carpeta de una biblioteca de ofertas o desde los resultados de búsqueda. También puede abrir una oferta desde una experiencia que utilice la oferta.

1. En la consola Ofertas, haga clic en el icono situado junto a la oferta y, a continuación, haga clic en **Editar**.
1. Añada los componentes a la oferta y edite el contenido como de costumbre.

## Eliminación de una oferta {#deleting-an-offer}

Elimine una oferta cuando ya no la necesite. Cuando intente eliminar una oferta que se utiliza en una experiencia, se le pedirá que confirme la eliminación. Al confirmar, se elimina la oferta y se elimina de las experiencias.

Puede eliminar una oferta mientras ve el contenido de cualquiera de las carpetas en una biblioteca de ofertas o los resultados de búsqueda.

1. En la consola Ofertas, haga clic en el icono situado junto a la oferta y seleccione **Eliminar**.

   Seleccione la oferta y haga clic en **Eliminar**.

1. En el cuadro de diálogo que aparece, haga clic en **Eliminar** para confirmar la eliminación.
1. Si la oferta se utiliza en una o más experiencias, aparece un cuadro de diálogo para indicar que se hace referencia a la oferta:

   * Para eliminar la oferta y quitarla de las experiencias, haga clic en **Forzar eliminación**.
   * Para conservar la oferta, haga clic en **Cancelar**.

## Búsqueda de ofertas {#searching-for-offers}

Busque ofertas de cualquier marca utilizando palabras clave para hacer coincidir el título.

![captura de pantalla_2019-03-05at124731](assets/screen-shot_2019-03-05at124731.png)

Los criterios de búsqueda actuales aparecen junto a los resultados. También puede ordenar los recursos en orden ascendente o descendente. Puede realizar una búsqueda desde todas las carpetas de cualquier biblioteca de ofertas. Los resultados de la búsqueda son los mismos independientemente de la carpeta actual.

Para buscar ofertas, haga lo siguiente:

1. En la parte superior de la consola Ofertas, haga clic en el icono de lupa. De forma predeterminada, la búsqueda se limita a las ofertas.
1. Escriba la palabra clave para buscar ofertas. Seleccione entre los resultados.
