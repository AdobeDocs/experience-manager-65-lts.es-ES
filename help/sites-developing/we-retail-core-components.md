---
title: Pruebe los componentes principales en We.Retail
description: Aprenda a trabajar con los componentes principales en Adobe Experience Manager mediante We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 62b6d299-f44e-4af3-b5e1-b0e92ca0598a
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 5%

---

# Pruebe los componentes principales de We.Retail{#trying-out-core-components-in-we-retail}

Los componentes principales son componentes modernos y flexibles que ofrecen una extensibilidad sencilla y permiten una integración sencilla en sus proyectos. Los componentes principales se han creado en torno a varios principios de diseño principales, como HTL, facilidad de uso predeterminada, configurabilidad, versiones y extensibilidad. El sitio `We.Retail` se ha creado en componentes principales.

## Pruébelo. {#trying-it-out}

1. Inicie Adobe Experience Manager (AEM) con el contenido de muestra `We.Retail` y abra la [Consola de componentes](/help/sites-authoring/default-components-console.md).

   **Navegación global > Herramientas > Componentes**

1. Al abrir el carril en la consola Componentes, puede filtrar para un grupo de componentes en particular. Los componentes principales se encuentran en

   * `.core-wcm`: los componentes principales estándar
   * `.core-wcm-form`: los componentes principales del envío de formularios

   Elija `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Todos los componentes principales utilizan el nombre **v1** para indicar la primera versión de cada componente. Está previsto lanzar versiones regulares, compatibles con AEM y que permiten una actualización sencilla para aprovechar las últimas funciones.
1. Haga clic en **Texto (v1)**.

   Observe que el **Tipo de recurso** del componente es `/apps/core/wcm/components/text/v1/text`. Los componentes principales se encuentran en `/apps/core/wcm/components` y se crean versiones por componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Haga clic en la ficha **Documentación** para ver la documentación para desarrolladores del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Vuelva a la consola Componentes. Filtre para el grupo **`We.Retail`** y seleccione el componente **Texto**.
1. Observe que el **Tipo de recurso** señala a un componente como se espera bajo `/apps/weretail`, pero el **Supertipo de recurso** señala al componente principal `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Haga clic en la ficha **Uso activo** para ver en qué páginas se utiliza este componente. Haga clic en la primera página de **Gracias** para editar la página.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. En la página de agradecimiento, seleccione el componente de texto y, en el menú de edición del componente, haga clic en el icono Cancelar herencia.

   [`We.Retail` tiene una estructura de sitio globalizada](/help/sites-developing/we-retail-globalized-site-structure.md) en la que el contenido se inserta desde el sitio de idioma principal a [live copies mediante un mecanismo denominado inheritance](/help/sites-administering/msm.md). Por este motivo, se debe cancelar la herencia para permitir que un usuario edite el texto manualmente.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Haga clic en **Sí** para confirmar la cancelación.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una vez cancelada la herencia y seleccionados los componentes de texto, hay muchas más opciones disponibles. Haga clic en **Editar**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ahora puede ver qué opciones de edición están disponibles para el componente de texto.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. En el menú **Información de la página**, seleccione **Editar plantilla**.
1. En el Editor de plantillas de la página, haga clic en el icono **Directiva** del componente Texto en el **Contenedor de diseño** de la página.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Los componentes principales permiten a un autor de plantillas configurar qué propiedades están disponibles para los autores de páginas. Estas propiedades incluyen funciones como fuentes de pegado permitidas, opciones de formato y estilos de párrafo disponibles.

   Estos cuadros de diálogo de diseño están disponibles para muchos componentes principales y funcionan en conjunto con el Editor de plantillas. Una vez activados, están disponibles para el autor a través de los editores de componentes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Consulte también {#further-information}

Para obtener más información sobre los componentes principales, consulte la guía de creación de [componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) para obtener una descripción general de las funcionalidades. Consulte la guía [Desarrollo de componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/overview) para obtener información general técnica.



Para obtener más información sobre los componentes principales, consulte el documento de creación [Componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) para obtener una descripción general de las funciones de los componentes principales y el documento para desarrolladores [Desarrollo de componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/overview) para obtener detalles técnicos.

Quizá también desee investigar [plantillas editables](/help/sites-developing/we-retail-editable-templates.md). Consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md) o el documento para desarrolladores Página [Plantillas - Editables](/help/sites-developing/page-templates-editable.md) para obtener información detallada sobre las plantillas editables.
