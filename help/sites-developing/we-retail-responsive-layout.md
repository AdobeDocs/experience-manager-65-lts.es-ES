---
title: Prueba del diseño interactivo en We.Retail
description: Aprenda a probar el diseño interactivo en Adobe Experience Manager mediante We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 6%

---

# Prueba del diseño interactivo en We.Retail{#trying-out-responsive-layout-in-we-retail}

Todas las páginas de We.Retail utilizan el componente Contenedor de diseño para implementar un diseño interactivo. El contenedor de diseño proporciona un sistema de párrafos que le permite colocar componentes en una cuadrícula adaptable. Esta cuadrícula puede reorganizar el diseño según el tamaño y el formato del dispositivo o la ventana. El componente se usa junto con el modo **Diseño** en el editor de páginas, lo que le permite crear y editar su diseño interactivo en función del dispositivo.

## Probando a cabo {#trying-it-out}

1. Edite la página Arctic Surfing en la sección Experiences de la rama maestra del idioma.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Cambie a **Vista previa** para ver la página tal como se representaría para un visitante del sitio web. Desplácese hacia abajo hasta el contenido del artículo *Espíritus Aloha en Noruega del Norte*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Cambie el tamaño de la ventana del explorador y observe cómo el diseño se adapta dinámicamente al cambio de tamaño.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Cambie al modo Diseño. La barra de herramientas del emulador se muestra automáticamente, lo que le permite planificar el diseño por dispositivo de destino.

   Al seleccionar un componente, se muestran las opciones flotantes y ocultas en el menú de edición junto con los controladores de tamaño del componente.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. Al pulsar y arrastrar el controlador de cambio de tamaño del componente, se muestra automáticamente la cuadrícula de diseño para ayudarle con el cambio de tamaño.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Información adicional {#further-information}

Para obtener más información, consulte el documento de creación [Diseño adaptable](/help/sites-authoring/responsive-layout.md) o el documento del administrador [Configuración del contenedor de diseño y el modo de diseño](/help/sites-administering/configuring-responsive-layout.md) para obtener detalles técnicos completos.
