---
title: Obtención de vista previa de páginas mediante los datos de ContextHub
description: La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub, le permite cambiar datos de los almacenes y resulta útil para obtener una vista previa del contenido
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 24%

---

# Obtención de vista previa de páginas mediante los datos de ContextHub{#previewing-pages-using-contexthub-data}

La barra de herramientas [ContextHub](/help/sites-developing/contexthub.md) muestra datos de los almacenes de ContextHub y le permite cambiar datos de los almacenes. La barra de herramientas de ContextHub resulta útil para obtener una vista previa del contenido determinado por los datos de un almacén de ContextHub.

La barra de herramientas consta de una serie de modos de interfaz de usuario que contienen uno o más módulos de interfaz de usuario.

* Los modos de interfaz de usuario son iconos que aparecen en la parte izquierda de la barra de herramientas. Al hacer clic en un icono, la barra de herramientas muestra los módulos de interfaz de usuario que contiene.
* Los módulos de IU muestran datos de uno o más almacenes de ContextHub. Algunos módulos de IU también permiten manipular los datos de almacenamiento.

ContextHub instala varios modos de interfaz de usuario y módulos de IU. Es posible que el administrador haya [configurado ContextHub](/help/sites-developing/ch-configuring.md) para que muestre otros.

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## Mostrar la barra de herramientas de ContextHub {#revealing-the-contexthub-toolbar}

La barra de herramientas de ContextHub está disponible en el modo de vista previa. La barra de herramientas solo está disponible en instancias de autor y únicamente si el administrador la ha activado.

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. Con la página abierta para edición, en la barra de herramientas, haga clic en Vista previa.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Para mostrar la barra de herramientas, haga clic en el icono de ContextHub.

   ![ContextHub](do-not-localize/screen_shot_2018-03-23at093621.png)

## Funciones del módulo de IU {#ui-module-features}

Cada módulo de interfaz de usuario proporciona un conjunto diferente de características, pero los siguientes tipos de características son comunes. Dado que los módulos de IU son ampliables, el desarrollador puede implementar otras funciones según sea necesario.

### Contenido de barra {#toolbar-content}

Los módulos de IU pueden mostrar datos de uno o más almacenes de ContextHub en la barra de herramientas. Los módulos de IU utilizan un icono y un título para identificarse.

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### Contenido emergente {#popup-content}

Algunos módulos de IU muestran una superposición emergente al pulsar o hacer clic en ellos. Normalmente, la ventana emergente contiene información adicional, aparte de lo que aparece en la barra de herramientas.

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### Forms emergente {#popup-forms}

La superposición emergente de un módulo puede incluir elementos de formulario que permiten cambiar los datos en el almacén de ContextHub. Si el contenido de la página está determinado por los datos de almacenamiento, puede utilizar el formulario y observar los cambios en el contenido de la página.

### Modo de pantalla completa {#fullscreen-mode}

Las superposiciones emergentes pueden incluir un icono en el que hacer clic para expandir el contenido emergente y cubrir toda la ventana o pantalla del explorador.

![Pantalla completa](do-not-localize/chlimage_1-18.png)
