---
title: Prueba de los componentes principales en We.Retail
description: Obtenga información sobre cómo probar los componentes principales en Adobe Experience Manager mediante We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Prueba de los componentes principales en We.Retail{#trying-out-core-components-in-we-retail}

Los componentes principales son componentes modernos y flexibles que ofrecen una extensibilidad sencilla y permiten una integración sencilla en sus proyectos. Los componentes principales se han creado en torno a varios principios de diseño principales, como HTL, facilidad de uso predeterminada, configurabilidad, versiones y extensibilidad. We.Retail se ha creado a partir de componentes principales.

## Probando a cabo {#trying-it-out}

1. Inicie Adobe Experience Manager (AEM) con el contenido de muestra de We.Retail y abra la [consola Componentes](/help/sites-authoring/default-components-console.md).

   **Navegación global > Herramientas > Componentes**

1. Al abrir el carril en la consola Componentes, puede filtrar para un grupo de componentes en particular. Los componentes principales se encuentran en

   * `.core-wcm`: los componentes principales estándar
   * `.core-wcm-form`: los componentes principales del envío de formularios

   Elija `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Todos los componentes principales se denominan **v1**, lo que refleja que esta es la primera versión de este componente principal. Las versiones regulares se lanzarán a partir de ahora, que serán compatibles con AEM y permitirán una actualización sencilla para que pueda aprovechar las últimas funciones.
1. Haga clic en **Texto (v1)**.

   Observe que el **Tipo de recurso** del componente es `/apps/core/wcm/components/text/v1/text`. Los componentes principales se encuentran en `/apps/core/wcm/components` y se crean versiones por componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Haga clic en la ficha **Documentación** para ver la documentación para desarrolladores del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Vuelva a la consola Componentes. Filtre por el grupo **We.Retail** y seleccione el componente **Text**.
1. Observe que el **Tipo de recurso** señala a un componente como se espera bajo `/apps/weretail`, pero el **Supertipo de recurso** señala al componente principal `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Haga clic en la ficha **Uso activo** para ver en qué páginas se utiliza este componente. Haga clic en la primera página de **Gracias** para editar la página.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. En la página de agradecimiento, seleccione el componente de texto y, en el menú de edición del componente, haga clic en el icono Cancelar herencia.

   [We.Retail tiene una estructura de sitio globalizada](/help/sites-developing/we-retail-globalized-site-structure.md) en la que el contenido se inserta desde los formatos de idioma a [Live Copies a través de un mecanismo denominado herencia](/help/sites-administering/msm.md). Por este motivo, se debe cancelar la herencia para permitir que un usuario edite el texto manualmente.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme la cancelación haciendo clic en **Sí**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una vez cancelada la herencia y seleccionados los componentes de texto, hay muchas más opciones disponibles. Haga clic en **Editar**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ahora puede ver qué opciones de edición están disponibles para el componente de texto.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. En el menú **Información de la página**, seleccione **Editar plantilla**.
1. En el Editor de plantillas de la página, haga clic en el icono **Directiva** del componente Texto en el **Contenedor de diseño** de la página.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Los componentes principales permiten a un autor de plantillas configurar qué propiedades están disponibles para los autores de la página. Estas incluyen funciones como fuentes de pegado permitidas, opciones de formato y estilos de párrafo disponibles.

   Estos cuadros de diálogo de diseño están disponibles para muchos componentes principales y funcionan en conjunto con el editor de plantillas. Una vez activados, están disponibles para el autor a través de los editores de componentes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Información adicional {#further-information}

Para obtener más información sobre los componentes principales, consulte el documento de creación [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) para obtener una descripción general de las capacidades de los componentes principales y el documento para desarrolladores [Desarrollo de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) para obtener una descripción general técnica.

Además, quizá desee investigar más a fondo [plantillas editables](/help/sites-developing/we-retail-editable-templates.md). Consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md) o el documento para desarrolladores Página [Plantillas - Editables](/help/sites-developing/page-templates-editable.md) para obtener información detallada sobre las plantillas editables.
